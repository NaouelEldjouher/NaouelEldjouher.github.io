---
layout: post
title: "Post 3: First HiFi Assembly: A Complete Chloroplast"
date: 2026-05-23
tags: [nextflow, aws, architecture, omniDomain]
---
Stub tests on PhytoFlow and FungalFlow caught architecture bugs early — 
Nextflow 26 breaking changes, a params block in the wrong config file, 
a Groovy reserved keyword. Fixed before any real data ran.

With the pipeline clean, PhytoFlow assembled a complete *Arabidopsis* 
chloroplast from 12,745 PacBio HiFi reads: 155,667 bp, 0 gaps, 100.8% 
expected size. The metrics reflected the biology exactly — high coverage 
with zero MapQ on the inverted repeats, 0% BUSCO because every BUSCO 
gene is nuclear-encoded.

The user selects the genome type --genome_type organelle and the pipeline automatically skips Helixer, MAKER, and NLR-Annotator. 
Next: nuclear genome.
