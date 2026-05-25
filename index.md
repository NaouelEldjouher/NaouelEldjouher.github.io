---
layout: none
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Naouel Eldjouher — Full-Stack Bioinformatician</title>
  <link rel="icon" type="image/png" href="/favicon.png">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg:      #0e0e0e;
      --surface: #161616;
      --border:  #242424;
      --accent:  #4ade80;
      --text:    #e2e2e2;
      --dim:     #888;
      --mono:    'JetBrains Mono', monospace;
      --sans:    'Inter', sans-serif;
    }
    html { scroll-behavior: smooth; }
    body { background: var(--bg); color: var(--text); font-family: var(--sans); font-weight: 300; line-height: 1.7; font-size: 15px; }
    a { color: inherit; text-decoration: none; }
    nav { position: fixed; top: 0; left: 0; right: 0; z-index: 50; background: rgba(14,14,14,0.92); backdrop-filter: blur(8px); border-bottom: 1px solid var(--border); }
    .nav-inner { max-width: 760px; margin: 0 auto; padding: 0 24px; height: 52px; display: flex; justify-content: space-between; align-items: center; }
    .nav-name { font-family: var(--mono); font-size: 0.8rem; color: var(--accent); }
    .nav-links { display: flex; gap: 24px; list-style: none; }
    .nav-links a { font-size: 0.8rem; color: var(--dim); transition: color 0.15s; }
    .nav-links a:hover { color: var(--text); }
    .page { max-width: 760px; margin: 0 auto; padding: 0 24px; }
    .hero { padding: 140px 0 100px; border-bottom: 1px solid var(--border); }
    .hero-badge { display: inline-block; font-family: var(--mono); font-size: 0.7rem; color: var(--accent); letter-spacing: 0.1em; margin-bottom: 24px; }
    h1 { font-size: clamp(2.2rem, 5vw, 3.2rem); font-weight: 300; line-height: 1.15; color: #fff; margin-bottom: 20px; letter-spacing: -0.02em; }
    .hero-desc { font-size: 1rem; color: var(--dim); max-width: 500px; margin-bottom: 36px; line-height: 1.8; }
    .hero-links { display: flex; gap: 12px; flex-wrap: wrap; }
    .link-btn { font-family: var(--mono); font-size: 0.75rem; padding: 8px 18px; border-radius: 3px; transition: all 0.15s; }
    .link-btn-solid { background: var(--accent); color: #0e0e0e; font-weight: 500; }
    .link-btn-solid:hover { opacity: 0.85; }
    .link-btn-outline { border: 1px solid var(--border); color: var(--dim); }
    .link-btn-outline:hover { border-color: #444; color: var(--text); }
    section { padding: 80px 0; border-bottom: 1px solid var(--border); }
    .section-label { font-family: var(--mono); font-size: 0.68rem; color: var(--dim); letter-spacing: 0.12em; text-transform: uppercase; margin-bottom: 40px; }
    .project { padding: 32px 0; border-top: 1px solid var(--border); display: grid; grid-template-columns: 1fr auto; gap: 20px; align-items: start; }
    .project:first-of-type { border-top: none; padding-top: 0; }
    .project-meta { font-family: var(--mono); font-size: 0.68rem; color: var(--dim); letter-spacing: 0.08em; margin-bottom: 8px; }
    .project-meta.current { color: var(--accent); }
    .project-name { font-size: 1.05rem; font-weight: 500; color: #fff; margin-bottom: 6px; }
    .project-stack { font-family: var(--mono); font-size: 0.7rem; color: var(--accent); margin-bottom: 14px; letter-spacing: 0.04em; }
    .project-points { padding-left: 16px; }
    .project-points li { color: var(--dim); font-size: 0.88rem; margin-bottom: 6px; line-height: 1.6; }
    .project-points li strong { color: var(--text); font-weight: 500; }
    .ext-link { font-family: var(--mono); font-size: 0.72rem; color: var(--dim); border: 1px solid var(--border); padding: 6px 14px; border-radius: 3px; white-space: nowrap; transition: all 0.15s; }
    .ext-link:hover { color: var(--accent); border-color: var(--accent); }
    .skills-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: 32px; }
    .skill-col-title { font-family: var(--mono); font-size: 0.7rem; color: var(--dim); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 16px; }
    .skill-list { list-style: none; }
    .skill-list li { font-size: 0.85rem; color: var(--dim); padding: 4px 0; border-bottom: 1px solid var(--border); }
    .skill-list li:last-child { border-bottom: none; }
    .log-item { display: flex; justify-content: space-between; align-items: flex-start; gap: 20px; padding: 24px 0; border-top: 1px solid var(--border); }
    .log-item:first-of-type { border-top: none; padding-top: 0; }
    .log-tag { font-family: var(--mono); font-size: 0.65rem; color: var(--accent); letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 6px; }
    .log-title { font-size: 0.95rem; color: var(--text); margin-bottom: 6px; font-weight: 500; }
    .log-excerpt { font-size: 0.83rem; color: var(--dim); line-height: 1.6; max-width: 520px; }
    .writing-item { display: flex; justify-content: space-between; align-items: center; gap: 20px; padding: 20px 0; border-top: 1px solid var(--border); }
    .writing-item:first-of-type { border-top: none; padding-top: 0; }
    .writing-title { font-size: 0.95rem; color: var(--text); margin-bottom: 4px; }
    .writing-sub { font-size: 0.8rem; color: var(--dim); }
    .contact-row { display: flex; gap: 12px; flex-wrap: wrap; }
    .contact-item { border: 1px solid var(--border); border-radius: 3px; padding: 14px 20px; transition: border-color 0.15s; }
    .contact-item:hover { border-color: #444; }
    .contact-item-label { font-family: var(--mono); font-size: 0.65rem; color: var(--dim); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 4px; }
    .contact-item-val { font-size: 0.85rem; color: var(--text); }
    footer { padding: 40px 0; text-align: center; font-family: var(--mono); font-size: 0.68rem; color: var(--dim); letter-spacing: 0.06em; }
    @media (max-width: 600px) {
      .skills-row { grid-template-columns: 1fr; gap: 24px; }
      .project { grid-template-columns: 1fr; }
      .log-item, .writing-item { flex-direction: column; }
      .nav-links { display: none; }
      h1 { font-size: 2rem; }
    }
  </style>
</head>
<body>
 
<nav>
  <div class="nav-inner">
    <span class="nav-name">naouel.dev</span>
    <ul class="nav-links">
      <li><a href="#logs">Logs</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#writing">Writing</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </div>
</nav>
 
<div class="page">
 
  <div class="hero">
    <div class="hero-badge">Open to opportunities</div>
    <h1>Naouel Eldjouher</h1>
    <p class="hero-desc">Full-Stack Bioinformatician specialising in plant and bacterial genomics, bridging high-throughput wet-lab insights with containerised, cloud-native infrastructure and Nextflow.</p>
    <div class="hero-links">
      <a href="#projects" class="link-btn link-btn-solid">Projects</a>
      <a href="https://github.com/NaouelEldjouher" class="link-btn link-btn-outline" target="_blank">GitHub ↗</a>
      <a href="https://linkedin.com/in/naoueleldjouher" class="link-btn link-btn-outline" target="_blank">LinkedIn ↗</a>
    </div>
  </div>
 
  <section id="logs">
    <p class="section-label">OmniDomain Build Logs</p>
    <div class="log-item">
      <div>
        <div class="log-tag">May 23, 2026</div>
        <div class="log-title">Post 3: First HiFi Assembly — A Complete Chloroplast</div>
        <div class="log-excerpt">Stub tests caught architecture bugs early — Nextflow 26 breaking changes, wrong config placement, a Groovy reserved keyword. PhytoFlow assembled a complete Arabidopsis chloroplast from 12,745 PacBio HiFi reads: 155,667 bp, 0 gaps, 100.8% expected size.</div>
      </div>
      <a href="/2026-05-23-omnidomain-day-3/" class="ext-link">Read ↗</a>
    </div>
    <div class="log-item">
      <div>
        <div class="log-tag">May 22, 2026</div>
        <div class="log-title">Post 2: Designing the Nextflow Repository Structure</div>
        <div class="log-excerpt">Three pipelines, one repo. Shared modules follow one rule: used by two or more pipelines go to modules/local/shared/. Write once, all pipelines inherit.</div>
      </div>
      <a href="/2026-05-22-omnidomain-Post2/" class="ext-link">Read ↗</a>
    </div>
    <div class="log-item">
      <div>
        <div class="log-tag">May 20, 2026</div>
        <div class="log-title">Post 1: The OmniDomain Blueprint</div>
        <div class="log-excerpt">After finishing NextAMR, expanding to fungi and plants. OmniDomain is a unified Nextflow + AWS Batch platform for bacterial, fungal, and plant genomics — one shared infrastructure, three pipeline engines.</div>
      </div>
      <a href="/2026-05-20-omnidomain-day-1/" class="ext-link">Read ↗</a>
    </div>
  </section>
 
  <section id="projects">
    <p class="section-label">Projects</p>
    <div class="project">
      <div>
        <div class="project-meta current">Current — In Progress</div>
        <div class="project-name">OmniDomain</div>
        <div class="project-stack">Nextflow DSL2 · AWS Batch · Docker · Terraform</div>
        <ul class="project-points">
          <li>Unified platform for <strong>bacterial, fungal, and plant genomics</strong> — one shared AWS infrastructure, three pipeline engines: NextAMR, FungalFlow, PhytoFlow.</li>
          <li>Shared module architecture means a bug fixed once is fixed everywhere. Already assembled a <strong>complete Arabidopsis chloroplast</strong> (155,667 bp, 0 gaps) from PacBio HiFi reads.</li>
        </ul>
      </div>
      <a href="https://github.com/NaouelEldjouher" class="ext-link" target="_blank">GitHub ↗</a>
    </div>
    <div class="project">
      <div>
        <div class="project-meta">01 — Cloud Pipeline</div>
        <div class="project-name">NextAMR (AMR-Flow)</div>
        <div class="project-stack">Nextflow DSL2 · AWS Batch · S3 · EC2 Spot · Docker · Terraform · Streamlit</div>
        <ul class="project-points">
          <li>Provisioned an <strong>event-driven AWS architecture</strong> with Terraform — automated job submission via AWS Batch, zero manual steps from upload to results.</li>
          <li>Cut cloud costs using <strong>EC2 Spot instances</strong>; full Docker containerisation for cross-platform reproducibility.</li>
          <li>End-to-end pipeline: FastP → Unicycler → Bakta → RGI/CARD, surfaced via a Streamlit dashboard.</li>
        </ul>
      </div>
      <a href="https://github.com/NaouelEldjouher/NextAMR" class="ext-link" target="_blank">GitHub ↗</a>
    </div>
    <div class="project">
      <div>
        <div class="project-meta">02 — M.Sc. Thesis</div>
        <div class="project-name">Baktflow</div>
        <div class="project-stack">Nextflow · Hybrid Assembly · Functional Annotation · Zenodo</div>
        <ul class="project-points">
          <li>End-to-end bacterial genomics workflow automating QC, <strong>short/long-read hybrid assembly</strong>, and downstream functional annotation.</li>
          <li>Core software deliverable for my M.Sc. thesis — archived on Zenodo, FAIR-compliant, openly accessible.</li>
        </ul>
      </div>
      <a href="https://zenodo.org/records/14995561" class="ext-link" target="_blank">Zenodo ↗</a>
    </div>
  </section>
 
  <section id="skills">
    <p class="section-label">Skills</p>
    <div class="skills-row">
      <div>
        <div class="skill-col-title">Bioinformatics</div>
        <ul class="skill-list">
          <li>NGS Analysis</li>
          <li>Bacterial Genomics</li>
          <li>Plant Genomics</li>
          <li>AMR Profiling</li>
          <li>GATK / Variant Calling</li>
          <li>FastP · Unicycler · Bakta</li>
        </ul>
      </div>
      <div>
        <div class="skill-col-title">Cloud & Workflow</div>
        <ul class="skill-list">
          <li>Nextflow DSL2</li>
          <li>AWS Batch · S3 · EC2</li>
          <li>Terraform (IaC)</li>
          <li>Docker</li>
          <li>Slurm HPC</li>
          <li>Bash Scripting</li>
        </ul>
      </div>
      <div>
        <div class="skill-col-title">Data & Dev</div>
        <ul class="skill-list">
          <li>Python · Pandas</li>
          <li>R · Tidyverse</li>
          <li>SQL</li>
          <li>Streamlit</li>
          <li>Git / GitHub</li>
        </ul>
      </div>
    </div>
  </section>
 
  <section id="writing">
    <p class="section-label">Writing</p>
    <div class="writing-item">
      <div>
        <div class="writing-title">From Terminal Scripts to the Cloud: Designing an Automated AMR Detection Platform</div>
        <div class="writing-sub">Medium · Deep-dive architectural breakdown of NextAMR</div>
      </div>
      <a href="/nextamr" class="ext-link">Read ↗</a>
    </div>
  </section>
 
  <section id="contact">
    <p class="section-label">Contact</p>
    <div class="contact-row">
      <a href="mailto:hellonaouel@gmail.com" class="contact-item">
        <div class="contact-item-label">Email</div>
        <div class="contact-item-val">hellonaouel@gmail.com</div>
      </a>
      <a href="https://linkedin.com/in/naoueleldjouher" class="contact-item" target="_blank">
        <div class="contact-item-label">LinkedIn</div>
        <div class="contact-item-val">naoueleldjouher</div>
      </a>
      <a href="https://github.com/NaouelEldjouher" class="contact-item" target="_blank">
        <div class="contact-item-label">GitHub</div>
        <div class="contact-item-val">NaouelEldjouher</div>
      </a>
      <a href="https://medium.com/@NaouelEldjouher" class="contact-item" target="_blank">
        <div class="contact-item-label">Medium</div>
        <div class="contact-item-val">@NaouelEldjouher</div>
      </a>
    </div>
  </section>
 
</div>
 
<footer>© 2026 Naouel Eldjouher · Full-Stack Bioinformatician · Giessen, DE</footer>
 
</body>
</html>
