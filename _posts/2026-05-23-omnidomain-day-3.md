---
layout: post
title: "Post 3: First HiFi Assembly: A Complete Chloroplast"
date: 2026-05-23
tags: [nextflow, aws, architecture, omniDomain]
---

Assembling plant organelle genomes is harder than it looks — most 
pipelines aren't built for it. Here's how PhytoFlow handled its first 
real HiFi dataset and what the results revealed about the pipeline's 
design.

Stub tests on PhytoFlow and FungalFlow caught architecture bugs early — 
Nextflow 26 breaking changes, a params block in the wrong config file, 
a Groovy reserved keyword. Fixed before any real data ran.

With the pipeline clean, PhytoFlow assembled a complete *Arabidopsis* 
chloroplast from 12,745 PacBio HiFi reads: 155,667 bp, 0 gaps, 100.8% 
expected size. The metrics reflected the biology exactly — high coverage 
with zero MapQ on the inverted repeats, 0% BUSCO because every BUSCO 
gene is nuclear-encoded.

The user selects the genome type --genome_type organelle and the pipeline 
automatically skips Helixer, MAKER, and NLR-Annotator. 

Baseline validated. Three things on the roadmap next:
1️⃣ The 100.8% artifact — resolving the overlapping assembler ends to cleanly circularize to 100.0%
2️⃣ Coverage saturation — at whole-genome scale, organelle coverage spikes to 5,000x+. Building a dynamic downsampler to prevent assembler crashes
3️⃣ Structural isomers — the .gfa assembly graph captures the two orientations of the chloroplast that a flat .fasta hides. Planning to expose this output Baseline nailed. Now making it scale.

Next: nuclear genome.
