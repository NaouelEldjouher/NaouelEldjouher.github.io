---
layout: post
title: "Post 2: Designing the Nextflow Repository Structure"
date: 2026-05-22
tags: [nextflow, aws, architecture, omniDomain]
---

How you structure a multi-pipeline repository determines everything 
that comes after — maintainability, debugging time, and whether shared 
code actually gets shared. Here's the structure I settled on for 
OmniDomain and why.

Three pipelines. One repo. The structure determines everything. Each 
pipeline gets its own main.nf and modules.config. One global 
nextflow.config handles profiles, resource limits and shared params.

Modules follow one rule:

Used by one pipeline → modules/local/{pipeline}/
Used by two or more → modules/local/shared/

Same rule for subworkflows. shared/repeat_masking runs RepeatModeler 
+ RepeatMasker for both FungalFlow and PhytoFlow. Write once. 
Both inherit it.
