---
layout: post
title: "OmniDomain: Building a Platform for Plant, Fungal, and Bacterial Genomics (Day 1)"
date: 2026-05-20
description: "An introduction to OmniDomain: Outlining what the three core pipelines will consist of, and the main technical challenges I expect to face."
---

# Blog Notes: Building OmniDomain (Day 1)

After finishing my work on **NextAMR**, I wanted to expand my research to include fungal and plant analysis, all in one place. To do this, I’m building **OmniDomain**: a central management platform that consolidates genomic analysis into a single, unified codebase. By leveraging a shared "control plane" powered by AWS Batch and a Streamlit dashboard, I’ve replaced the model of one-off pipelines with a standardized framework. This treats infrastructure as a reusable utility—meaning any improvement in storage, processing, or pipeline logic is instantly inherited across all research areas, allowing me to focus on the science rather than the setup.


### The Scope & Challenge
To scale successfully, my architecture must accommodate vastly different biological requirements:

| Engine | Target | Genome Size | Key Challenge |
| :--- | :--- | :--- | :--- |
| **NextAMR** | Bacteria | 2–6 Mb | AMR gene detection, plasmid resolution |
| **FungalFlow** | Fungi | 20–80 Mb | Gene prediction, BGC discovery |
| **PlantFlow** | Plants | 100 Mb – 16 Gb | Polyploidy, 40–85% repeat content |

---

### The Blueprint
I am using my **NextAMR** pipeline as the foundation, porting its engine—global `nextflow.config` files, retry logic, and subworkflow abstractions—to create a "Base Architecture" that works across kingdoms.

**Core Focus Areas:**
*   **Infrastructure Inheritance:** Improving a container strategy or fixing a memory bug in one pipeline instantly updates the entire ecosystem.
*   **Modular Subworkflows:** Abstracting repetitive tasks (QC, repeat masking) into shared, reusable logic.
*   **AWS Cost Management:** Utilizing Spot instance strategies, S3 intelligent storage, and resource profiling to balance performance with exponentially scaling data costs.

---

### Current Status
*   **🧬 Metacflow:** Stable foundation for metagenomics.
*   **🌱 OmniFlora:** Testing plant HiFi assembly architecture.
*   **🍄 FungalFlow:** Scaling assembly and BGC detection.


---

### The Learning Curve
Designing an `nf-core` module system flexible enough to handle bacterial binning while remaining robust enough for complex plant assemblies is a significant architectural challenge. Coming from a bacterial-focused background, scaling my logic to the eukaryotic domain—where genome sizes and repeat content require drastically different computational approaches—is my biggest hurdle.

---

### What's Next?
I’ve started the **Technical Design Document (TDD)** to map out the infrastructure. Future notes will cover:
1.  **Nextflow Architecture:** Folder structures and module scopes.
2.  **Streamlit Control Plane:** Building the unified UI.
3.  **AWS Infrastructure:** Terraform configurations for cost-efficient compute.

I’m "learning in public." The goal isn't perfection, but building a system I can actually maintain.

**Follow the progress:** [github.com/NaouelEldjouher](https://github.com/NaouelEldjouher)


