# A Lightweight NGS Variant‑Calling Pipeline (chr20)

## Project intent (learning‑phase)

This repository documents a **learning‑focused, chromosome‑restricted NGS variant‑calling workflow** built on **chromosome 20** using real Illumina sequencing data (SRR1910621).

The goal of this project is **not** to present a production‑ready or genome‑wide pipeline. Instead, it represents a **deliberate learning exercise** to understand how each major step in a variant‑calling workflow behaves, how results should be sanity‑checked, and how large sequencing data can be handled responsibly during early experimentation.

This repository complements my full exome project (**From‑FASTQ‑to‑Annotated‑Variants‑A‑Human‑Exome‑Pipeline**). While the exome pipeline demonstrates end‑to‑end completeness, this chr20 project reflects my **earlier, exploratory learning stage**, where speed, clarity, and interpretability were prioritized.

---

## Why chromosome 20?

Analysis of chromosome 20 was a **simplification choice** because it:

* Enables faster execution and iteration on modest hardware
* Reduces memory and storage requirements
* Makes debugging and result inspection manageable
* Still preserves biologically meaningful variation
  
---

## What this pipeline does

The workflow covers the core steps of short‑read variant calling:

* Raw FASTQ quality control and trimming
* Alignment to a chr20‑only GRCh38 reference
* Sorting, indexing, and duplicate marking
* Single‑sample variant calling
* Explicit variant filtering
* Basic variant statistics and density analysis

Each step was run manually and inspected, with an emphasis on **learning what can go wrong and how outputs should be interpreted**.

---

## Tools used and the reasoning

* **fastp** – simple, integrated read QC and trimming with clear before/after reports
* **bwa mem** – widely used short‑read aligner suitable for human data
* **samtools** – essential BAM processing and alignment QC
* **Picard** – duplicate marking to understand PCR artifact handling
* **bcftools** – transparent, pileup‑based single‑sample variant calling and filtering
* **bedtools** – basic genomic windowing for exploratory density analysis

These tools were chosen because they are **well‑established, widely documented, and suitable for learning fundamental concepts**.

---

## Results and sanity checks

Variant calling was intentionally followed by **basic statistical checks** rather than downstream interpretation.

From `bcftools stats` on the filtered chr20 VCF:

* Total variants: **1,969**

  * SNPs: 1,943
  * Indels: 26
* Ti/Tv ratio: **~0.52**
* Most variant sites have **low depth (DP = 1–2)**

### How these results were interpreted

* The small number of variants is expected for a chromosome‑restricted analysis
* The low Ti/Tv ratio reflects **single‑sample calling with shallow per‑site depth**, and was confirmed not to be a pipeline error
* These metrics were used as **learning‑oriented sanity checks**, not as genome‑wide quality benchmarks

Understanding why these values differ from textbook expectations was a key learning outcome of this project.

---

## Variant density analysis

Variants were summarized in **100 kb windows across chr20** to explore how calls are distributed along the chromosome.

This step was included to:

* Practice basic genomic interval operations
* Learn how variant density can highlight uneven coverage or technical artifacts
* Go beyond “file generation” and perform simple exploratory analysis

---

## Handling large sequencing data

This repository intentionally excludes:

* Raw FASTQ files
* BAM files
* Full VCF outputs

Only lightweight, information‑dense artifacts (QC reports, statistics, BED files) are tracked.

This reflects an important practical lesson: **real NGS data are large and must be handled carefully**, even during learning‑phase projects.

---

## What went wrong and what I learned

During this project, I encountered several issues typical of early pipeline work:

* Reference mismatches when using chromosome‑restricted FASTA files
* Unexpected depth distributions that required careful interpretation
* Memory limitations during alignment on local systems

Resolving these issues helped me understand:

* Why explicit filtering is necessary in single‑sample analyses
* Why many quality metrics are context‑dependent
* Why small, controlled experiments are useful before scaling up

---

## Relationship to my exome pipeline

This chr20 project should be viewed as a **learning‑stage companion** to my full exome pipeline:

* **chr20 pipeline:** exploration, debugging, statistics, and concept‑building
* **exome pipeline:** complete, reproducible FASTQ → annotated VCF workflow

Together, they reflect my progression from **learning core mechanics** to **executing a full NGS analysis responsibly**.

---

## Scope and limitations

* Single sample only
* Chromosome‑restricted
* No joint genotyping or variant recalibration
* No clinical interpretation

These limitations are intentional and aligned with the learning goals of the project.

---

## Closing note

This repository represents an **honest snapshot of my learning process** in bioinformatics. It prioritizes clarity, reasoning, and reflection over sophistication, and serves as a foundation for more advanced analyses in subsequent projects.
