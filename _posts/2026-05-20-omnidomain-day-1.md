---
layout: post
title: "Day 1: The OmniDomain Blueprint"
date: 2026-05-20
---

After finishing **NextAMR**, I’m expanding my cloud infrastructure to handle fungal and plant genomes. I'm building **OmniDomain**: a unified Nextflow & AWS Batch control plane. 

**The Challenge:** Scaling from 5Mb bacterial genomes to 16Gb polyploid plant genomes requires entirely different compute strategies. 

**The Goal:** Shared infrastructure inheritance. If I optimize S3 storage or fix a memory bug in the bacterial pipeline, the eukaryotic pipelines inherit the fix instantly. 

**Current Status:**
* 🧫 **Metacflow** — Bacterial metagenomics (Stable)
* 🍄 **FungalFlow** — Fungal genome assembly, BGC detection, and secretome (In development)
* 🌱 **PhytoFlow** — Plant HiFi assembly, structural, and functional annotation (Architecting now)

*Technical Design Document (TDD) is currently in progress!*
**Follow the progress:** [github.com/NaouelEldjouher](https://github.com/NaouelEldjouher)


