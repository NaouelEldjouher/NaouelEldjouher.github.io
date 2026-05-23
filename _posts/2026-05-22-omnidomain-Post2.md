---
layout: post
title: "Designing the Nextflow repository structure"
date: 2026-05-22
tags: [nextflow, aws, architecture, omniDomain]
---
**Three pipelines. One repo. The structure determines everything.**
Each pipeline gets its own `main.nf` and `modules.config`. 
One global `nextflow.config` handles profiles, resource limits, 
and shared params.
### Modules follow one rule:
**Used by one pipeline** → `modules/local/{pipeline}/`
**Used by two or more** → `modules/local/shared/`
Same rule for subworkflows. `shared/repeat_masking` runs 
For example: RepeatModeler + RepeatMasker for both FungalFlow and PhytoFlow.
**Write once. Both inherit it.**
---
[github.com/NaouelEldjouher](https://github.com/NaouelEldjouher)
