---
layout: post
title: "PhytoFlow Case 3 — Nuclear + Reference: What Changes When You Add a Reference Genome"
date: 2026-06-02
tags: [nextflow, aws, architecture, omnidomain, plantgenomics, hifi]
---

Same data as Case 2. Same 5,000 PacBio HiFi reads from *Arabidopsis thaliana* (ENA: ERR8666127, average 18,236bp). Same 2.1Mb partial assembly.

One change: `--reference arabidopsis_reference.fna.gz`

That single flag switches the entire annotation strategy.

---

## How PhytoFlow routes itself

The pipeline decides which tools to run based on two flags. No manual tool selection. No config editing.

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

---

## What the pipeline auto-detected

By providing `--genome_type nuclear` and `--reference ref.fna`, the pipeline instantly configured its state:

* `do_maker = true`
* `do_helixer = false`
* RagTag scaffolding enabled
* BRAKER3 enabled, Helixer disabled

No other flags. The pipeline routes itself.

---

## RagTag scaffolding — what happened

RagTag attempted to order 38 assembled contigs against the TAIR10 *Arabidopsis* reference (135Mb, 5 chromosomes).

With only 2.1Mb of assembly — roughly 1.5% of the full genome — most contigs could not be confidently placed. RagTag requires sufficient overlap between the query assembly and the reference to anchor contigs. 

This is not a pipeline failure. RagTag ran without errors and produced correct output. The limited scaffolding is a direct consequence of using a validation dataset — 5,000 reads representing 1.5% of the genome. On a complete assembly, RagTag would anchor thousands of contigs into five chromosome-scale scaffolds.

---

## Why MAKER was replaced with BRAKER3

The original Case 3 design used MAKER for evidence-based gene prediction. MAKER is the traditional choice — it takes a masked assembly and protein hints and produces high-quality gene models.

MAKER also requires the DFam repeat database. The public biocontainers Docker image does not bundle it. Rather than mount a 15GB database as a volume — fragile, not portable, breaks on AWS — I replaced MAKER with BRAKER3.

BRAKER3 is MAKER's modern successor. Same concept: protein evidence to anchor gene predictions, without the DFam dependency. It is what most new plant genome papers now use.

---

## The four bugs on the way

These are documented for anyone hitting the same issues — BRAKER3's documentation does not surface them clearly.

**Bug 1 — wrong flag name**
BRAKER3 does not have a `--cores` flag. It uses `--threads`. Exit 255 with `Unknown option: cores`.

**Bug 2 — gzipped input rejected**
BRAKER3 requires plain FASTA protein input. The test data is `.faa.gz`. Fixed by adding `gunzip -c` before passing proteins to BRAKER3.

**Bug 3 — wrong output filename**
The process expected `braker/braker.gff3`. BRAKER3 actually outputs `braker/braker.gtf`. Fixed the output directive. AGAT handles GTF natively so no format conversion needed.

**Bug 4 — missing channel assignment**
BRAKER3 ran successfully but `ch_maker_gff = BRAKER3.out.gff` was never written in `annotation_structural.nf`. `EXTRACT_PROTEOME` waited for a GFF channel that was always empty. One line fix.

---

## Gene prediction results

> **BRAKER3 proteins:** 770
> **Helixer proteins:** 527 (Case 2, same reads)
> **Increase:** +46%

770 proteins from the same 2.1Mb assembly that gave 527 with Helixer. The difference is protein evidence.

BRAKER3 uses *Arabidopsis* protein hints to validate and anchor predictions. Where Helixer predicts from sequence patterns alone, BRAKER3 asks: *does this predicted gene match a known Arabidopsis protein?* If yes, confidence increases. If a region has protein support but Helixer missed it, BRAKER3 finds it.

The 13,508 GTF feature lines include genes, transcripts, CDS, exons, and UTRs — approximately 2,700–3,400 distinct gene models, consistent with *Arabidopsis* gene density at this assembly size.

---

## What this validates

Case 3 confirms that the pipeline correctly:
* Routes to BRAKER3 when `--reference` is provided.
* Disables Helixer automatically.
* Runs RagTag scaffolding before annotation.
* Produces more gene models with protein evidence than without.
* Handles GTF output from BRAKER3 without format conversion.

---

## The three cases compared

| Metric | Case 1 | Case 2 | Case 3 |
| :--- | :--- | :--- | :--- |
| **Data** | Organelle HiFi | 5k nuclear HiFi | 5k nuclear HiFi |
| **Extra input** | None | None | TAIR10 reference |
| **Scaffolding** | Skipped | Passthrough | RagTag |
| **Gene predictor** | None | Helixer | BRAKER3 |
| **Proteins predicted** | 0 | 527 | 770 |
| **Key finding** | 100.8% chloroplast | AGL18 detected | +46% with evidence |

---
*Next: module architecture refactor, then FungalFlow validation.*

[← Back to Home](/)

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true, theme: 'dark' });
</script>
