---
layout: post
title: "Post 4: PhytoFlow Case 2 — Nuclear Genome: What the Biology Says"
date: 2026-05-29
tags:
  - nextflow
  - aws
  - plantgenomics
  - omniDomain
  - hifi
---

With the organelle case validated, PhytoFlow moved to its first 
nuclear genome run. The goal was not a publishable genome, it 
was a pipeline validation: does the tool selection logic work, 
and does the output reflect real plant biology?



---

## How PhytoFlow routed itself

One flag triggers the entire nuclear analysis mode. No manual 
tool selection. No config editing.

<pre class="mermaid" style="display: flex; justify-content: center; margin: 40px 0; background: transparent; border: none;">
graph TD
    A[Input: HiFi Reads] --> B[--genome_type nuclear]
    B --> C[Hifiasm Assembly]
    C --> D[Coverage + MapQ QC]
    D --> E{reference provided?}
    E -->|No| F[Helixer gene prediction]
    F --> G[eggNOG-mapper]
    G --> H[527 proteins predicted\n62.6% annotated\nAGL18 detected]
    E -->|Yes| I[RagTag + BRAKER3\nCase 3]
</pre>

---

## The data

5,000 PacBio HiFi reads from *Arabidopsis thaliana* 
(ENA: ERR8666127), average length 18,236bp. A deliberately 
small dataset — the goal was pipeline validation, not a 
publishable genome.

---

## Assembly results

Hifiasm produced 38 contigs totalling 2.1Mb. All 38 passed 
the Helixer minimum length filter (≥21kb) — the first 
biological checkpoint. Sequences too short do not have enough 
context for deep learning gene prediction.

---

## What coverage reveals

Two contigs stood out: high coverage (73-162x) with low MapQ 
(~3). High coverage combined with low mapping quality is the 
signature of repetitive or organelle sequence. Plant HiFi reads 
always contain chloroplast and mitochondrial DNA — these contigs 
are likely organelle fragments assembled alongside nuclear 
sequence.

The remaining contigs showed 2-25x coverage with MapQ 45-60 — 
the expected signature of unique nuclear sequence at low read 
depth.

---

## Gene prediction

Helixer predicted 527 proteins from 2.1Mb of sequence — 
approximately one gene per 4kb, consistent with the known 
*Arabidopsis* gene density of one gene per 4.5kb. The prediction 
density alone suggests these are real genes.

---

## Functional annotation

eggNOG-mapper annotated 330 of 527 proteins (62.6%) with GO 
terms. The most represented pathway was MAP kinase signalling — 
*Arabidopsis* stress response genes. This makes biological sense 
for a partial assembly where stress-responsive loci are enriched.

Two genes stood out as validation signals:

**AGL18** : a MADS-box transcription factor controlling floral 
development. AGL18 specifically acts as a floral repressor. Its 
detection in a 2.1Mb partial assembly from 5,000 reads is a 
strong validation signal — it is a well-characterised gene with 
a distinctive domain signature that Helixer and eggNOG both 
correctly identified.

**TFIIB**  :  transcription initiation factor B. Core transcription 
machinery, conserved across all eukaryotes. Its presence confirms 
the assembly contains genuinely nuclear sequence, not just 
organelle or repetitive DNA.

---

## NLR-Annotator

Zero NLR loci detected. This is expected — NBS-LRR disease 
resistance genes are large, multi-domain proteins that require 
substantial nuclear contigs to be detected. With 2.1Mb of partial 
assembly the statistical power is not there. On a complete 
*Arabidopsis* genome you would expect approximately 150 NLR 
candidates.

---

## What this validates

Case 2 confirms that the pipeline correctly:

- Auto-detects nuclear de novo mode from `--genome_type nuclear`
- Enables Helixer, disables MAKER automatically
- Skips scaffolding when no reference or Hi-C data is provided
- Predicts biologically plausible genes at the correct density
- Annotates known *Arabidopsis* genes with correct functions

---

## The three cases so far

| | Case 1 | Case 2 |
|---|---|---|
| Data | Organelle HiFi | 5k nuclear HiFi |
| Extra input | None | None |
| Gene predictor | None | Helixer |
| Proteins predicted | 0 | 527 |
| Key finding | 100.8% chloroplast | AGL18 detected |

Next: Case 3 — nuclear + reference mode with BRAKER3.

---

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true, theme: 'dark' });
</script>

[← Back to Home](/)
