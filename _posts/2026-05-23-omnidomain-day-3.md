---
layout: post
title: "Post 3: PhytoFlow — First HiFi Assembly and How the Pipeline Routes Itself"
date: 2026-05-23
tags:
  - nextflow
  - aws
  - architecture
  - omniDomain
  - plantgenomics
  - hifi
---

OmniDomain now has three new pipelines under active development: 
PhytoFlow for plant genome assembly and annotation, FungalFlow 
for fungal genome assembly and biosynthetic gene cluster discovery, 
and MetaCflow for bacterial shotgun metagenomics and MAG recovery. 
All three share the same AWS infrastructure, Terraform provisioning, 
and Nextflow DSL2 architecture.

Before running any real data, all three pipelines went through 
stub testing — running the full pipeline graph with minimal inputs 
to catch architecture bugs before any real compute ran. Three issues 
surfaced across PhytoFlow and FungalFlow and were resolved: Nextflow 
26 breaking changes in process syntax, a `params` block placed in 
the wrong config file, and a Groovy reserved keyword conflict in a 
process name.

In this post I introduce PhytoFlow and document its first real 
validation run,assembling a complete *Arabidopsis* chloroplast 
from PacBio HiFi reads.

---

## How PhytoFlow routes itself

<pre class="mermaid" style="display: flex; justify-content: center; margin: 40px 0; background: transparent; border: none;">
graph TD
    A[Input: HiFi Reads] --> B{genome_type?}
    B -->|organelle| C[Hifiasm Assembly]
    C --> D[Skip Annotation]
    D --> E[BUSCO + Coverage QC]
    E --> F[Complete chloroplast\n155,667bp, 0 gaps]

    B -->|nuclear| G[Hifiasm Assembly]
    G --> H{reference provided?}

    H -->|No| I[Helixer]
    I --> J[eggNOG-mapper]
    J --> K[527 proteins\n62.6% annotated\nAGL18 detected]

    H -->|Yes| L[RagTag Scaffolding]
    L --> M[BRAKER3]
    M --> N[eggNOG-mapper]
    N --> O[770 proteins\n+46% vs Helixer]
</pre>

This post documents Case 1 — organelle mode. Cases 2 and 3 
follow in the next posts.

---

## Architecture bugs caught before real data ran

Before running any real data, stub tests on PhytoFlow and 
FungalFlow caught several architecture bugs early:

- Nextflow 26 breaking changes in process syntax
- A `params` block placed in the wrong config file
- A Groovy reserved keyword conflict in a process name

All fixed before anything real ran. Catching bugs at the 
architecture level — before compute costs accumulate — is one 
of the core design principles of OmniDomain.

---

## The data

12,745 PacBio HiFi reads from *Arabidopsis thaliana* 
(ENA: ERR8666127). Organelle mode selected with a single flag: 
`--genome_type organelle`.

---

## What the pipeline auto-detected

`--genome_type organelle` triggered automatic configuration:

- Helixer disabled — gene prediction is for nuclear genomes
- MAKER disabled — same reason
- NLR-Annotator disabled — disease resistance genes are nuclear
- BUSCO run in organelle mode
- Coverage QC applied with organelle thresholds

No manual tool selection. No config editing.

---

## Assembly results

Hifiasm assembled a complete *Arabidopsis* chloroplast:

- **155,667bp** — 100.8% of the expected chloroplast size
- **0 gaps** — fully contiguous
- **0% BUSCO** — correct, because every BUSCO gene is 
  nuclear-encoded. A 0% organelle BUSCO score is not a 
  failure — it is the expected result.

The 100.8% overshoot is a known assembler artifact from 
overlapping ends at the circular junction. The assembly is 
biologically correct — the overlap needs to be resolved to 
produce a clean circularisation.

---

## What coverage reveals

High coverage with zero MapQ on two regions — the inverted 
repeats. This is the expected chloroplast signature. Inverted 
repeats are identical sequences that exist twice in the 
chloroplast genome. Reads mapping to them have zero mapping 
quality because the aligner cannot distinguish which copy 
they came from.

The pipeline correctly identified and flagged these regions 
without manual intervention.

---

## Three things on the roadmap

**1. The 100.8% artifact**
Resolving the overlapping assembler ends to cleanly circularise 
to 100.0%. This requires trimming the duplicate junction sequence 
and confirming the circular topology.

**2. Coverage saturation**
At whole-genome scale, organelle reads spike to 5,000x or higher. 
Building a dynamic downsampler to prevent assembler crashes on 
high-coverage organelle input.

**3. Structural isomers**
The `.gfa` assembly graph captures the two orientations of the 
chloroplast large single-copy region — a biological reality that 
a flat `.fasta` hides. Planning to expose this output for 
downstream structural analysis.

---

Baseline validated. Next: nuclear genome — Case 2.

---


<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true, theme: 'dark' });
</script>

[← Back to Home](/)
