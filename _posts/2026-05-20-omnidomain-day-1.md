---
layout: post
title: "Post 1: The OmniDomain Blueprint"
date: 2026-05-20
tags: [nextflow, aws, architecture, omniDomain]
---

Building one pipeline is straightforward. Building three that share 
infrastructure without duplicating bugs is a different problem 
entirely. This is why I built OmniDomain.

After finishing NextAMR, I'm expanding to fungi and plants.
OmniDomain is a unified Nextflow + AWS Batch platform for
bacterial, fungal, and plant genomics — one shared infrastructure,
three pipeline engines.

The core idea: fix a memory bug once, all pipelines inherit it.

Current status:

---

* **🦠 NextAMR** bacterial WGS + AMR detection (published)
* **🍄 FungalFlow** fungal assembly + BGC detection (building)
* **🌱 PhytoFlow** plant HiFi assembly + annotation (architecting)
* **🧬 Metacflow** bacterial metagenomics (v2.0)

---
