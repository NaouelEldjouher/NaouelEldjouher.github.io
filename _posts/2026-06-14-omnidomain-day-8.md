---
title: "First route end to end: FastAPI, JWT auth, and the service layer"
date: 2026-06-14
tags: [omnidomain, fastapi, jwt, pydantic, pytest]
---

Data layer done. Next: the FastAPI application, authentication, and the first real routes.

The goal was to wire the full request path end to end. A scientist sends a POST request, gets back a run ID. That means: validate the request, authenticate the user, call the service, call the repository, submit to AWS Batch, return a response. Every layer doing exactly one thing.

<pre class="mermaid" style="display: flex; justify-content: center; margin: 100px 0; background: transparent; border: none; transform: scale(1.5); transform-origin: center;">
sequenceDiagram
    actor S as Scientist
    participant UI as Streamlit
    participant API as FastAPI
    participant Auth as auth_service
    participant Svc as run_service
    participant Repo as repository
    participant DB as PostgreSQL
    participant Batch as AWS Batch

    S->>UI: fills form, clicks Submit
    UI->>API: POST /runs (Bearer token)
    API->>Auth: validate JWT token
    Auth-->>API: current_user
    API->>Svc: create_run()
    Svc->>Svc: validate TSV inputs
    Svc->>Repo: RunRepository.create()
    Repo->>DB: INSERT runs + status_history (flush)
    Svc->>Batch: submit_job()
    Batch-->>Svc: job_id
    Svc->>Repo: mark_submitted()
    Repo->>DB: UPDATE runs (flush)
    Svc->>DB: db.commit()
    API-->>UI: RunResponse (run_id, status=SUBMITTED)
    UI-->>S: redirects to monitor tab
</pre>

---

**main.py — the entry point**

One file, three jobs: configure logging, register middleware, mount routes. The lifespan context manager handles startup and shutdown. CORS is configured to allow the Streamlit UI at `localhost:8501` to call the API — without this the browser blocks cross-origin requests.

A `/health` endpoint with no authentication gives the load balancer and CI a way to verify the API is running without needing credentials.

---

**schemas.py — Pydantic request and response models**

Every route has an explicit input schema and output schema. FastAPI validates incoming JSON against the input schema automatically — wrong type, missing required field, invalid email format — the request is rejected before any service code runs. The error message tells the caller exactly what's wrong.

Response schemas control what gets returned. Sensitive fields never appear in responses because they're simply not in the schema.

---

**Auth — email-only JWT**

For internal scientific tooling, password management adds complexity without much security benefit. Scientists log in with their institutional email. First visit creates an account. Subsequent visits return the same user.

The service creates a JWT token with the user ID and email, signed with a secret key, expiring after 24 hours. Every protected route validates this token via a FastAPI dependency:

```python
@router.get("/runs/")
def list_runs(
    db: Session = Depends(get_db),
    current_user: User = Depends(get_current_user),  # JWT validated here
):
    return run_service.get_user_runs(db, current_user.user_id)
```

`Depends(get_current_user)` tells FastAPI: before calling this function, validate the token and inject the user. The route never sees invalid tokens.

---

**run_service.py — where business logic lives**

The service layer is the part most developers skip. Logic ends up in routes, in repositories, scattered. The result: untestable, hard to change.

`run_service.py` does three things in order:

1. Validate the scientific inputs — check TSV structure before touching the database
2. Create the run record via the repository
3. Submit to AWS Batch, update the run with the job ID

The transaction commits only after all three succeed. If Batch submission fails, the database rolls back — no orphaned run records with missing job IDs.

---

**Testing without AWS**

The test suite runs entirely in SQLite in-memory — no Docker, no Postgres, no AWS credentials needed. Repository tests verify SQL logic. Route tests mock AWS Batch:

```python
with patch("api.services.run_service.boto3") as mock_boto3:
    mock_batch = MagicMock()
    mock_batch.submit_job.return_value = {"jobId": "aws-job-123"}
    mock_boto3.client.return_value = mock_batch
    # test the route without touching AWS
```

This is what testable architecture looks like in practice. The service layer calls boto3, the test replaces boto3 with a mock. The route and service logic is tested, AWS costs nothing.

CI now runs two parallel jobs: API tests on SQLite, UI tests on Postgres with Alembic migrations.

---

*Next: monitor service, Streamlit calling the API, deployment to ECS.*

*Code → [github.com/NaouelEldjouher/OmniDomain]*


<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true, theme: 'dark' });
</script>
