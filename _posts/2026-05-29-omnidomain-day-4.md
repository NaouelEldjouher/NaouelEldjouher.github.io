---
layout: post
title: "Post 4: PhytoFlow Nuclear Pipeline — First Full Run"
date: 2026-05-29
tags: [nextflow, aws, plantgenomics, omniDomain]
---

A plant genome pipeline that works is one thing. One that 
interprets its own results is another. Here's what PhytoFlow's 
first nuclear run revealed.

5,000 PacBio HiFi reads. 38 contigs. 2.1Mb. All 15 processes 
green in 50 minutes.

─ What the biology says ─

Two contigs showed 73-162x coverage with MapQ ~3 — the signature 
of organelle sequence mixed into a nuclear assembly. Expected. 
Plant HiFi reads always contain chloroplast DNA. The remaining 
contigs showed 2-25x coverage with MapQ 50-60 — clean nuclear 
sequence.

Helixer predicted 527 proteins at ~1 gene per 4kb — consistent 
with Arabidopsis gene density. eggNOG-mapper annotated 62.6% 
with GO terms.

Two genes confirmed the pipeline is predicting real biology:
→ AGL18 — MADS-box floral repressor, well-characterised in 
   Arabidopsis
→ TFIIB — core transcription factor, conserved across all 
   eukaryotes

─ What the pipeline auto-detected ─

One flag: --genome_type nuclear
Helixer enabled. MAKER skipped. YAHS skipped.
Correct tool selection. No manual configuration.

Next: nuclear + reference mode using MAKER.
