# Cancer Somatic Variant Calling: A Technical Learning Case Study

![Status](https://img.shields.io/badge/Status-Technical%20Literacy-blue)
![Field](https://img.shields.io/badge/Field-Clinical%20Genomics-orange)
![Goal](https://img.shields.io/badge/Goal-AI%20Data%20Foundations-green)

A technical learning repository focused on mapping the clinical-grade somatic 
variant calling pipeline used in precision oncology. 

Developed by a molecular biologist with first-author RNA-Seq experience 
(PLOS NTDs, 2020) to build a grounded understanding of the genomic data 
structures that underpin biomedical AI systems.

---

## Motivation

Cancer genomics is the engine of precision oncology. Understanding the somatic 
variant discovery process—identifying mutations acquired by tumour cells is 
essential for accurately interpreting targeted therapy selection and diagnostic 
reporting.

This work serves as a **technical case study** and **learning repository** 
mapping the GATK Best Practices for somatic short variant discovery. **I am 
developing this technical literacy to provide a grounded biological foundation 
for my broader research into the social and ethical governance of biomedical AI.**

---

## Technical Scope: The Somatic Pipeline

This case study follows the "Tumour-with-Matched-Normal" logic, essential for 
distinguishing acquired somatic mutations from inherited germline variants.

| Detail | Information |
|---|---|
| Sample | HCC1143 breast cancer cell line |
| Type | Tumour + matched normal pair |
| Reference | GRCh38 / hg38 |
| Sequencing | Whole exome sequencing (WES) |
| Data | Open access tutorial dataset (Broad Institute) |

---

## Pipeline Overview (Conceptual Mapping)

1. **Alignment:** BWA-MEM → Mapping raw FASTQ to the GRCh38 reference.
2. **BAM Processing:** SAMtools + Picard (sorting, indexing, marking duplicates).
3. **Calibration:** GATK BQSR (Base Quality Score Recalibration).
4. **Variant Calling:** GATK Mutect2 (Somatic-specific discovery logic).
5. **Filtering:** GATK FilterMutectCalls (Distinguishing true variants from noise).
6. **Annotation:** ANNOVAR + COSMIC + OncoKB (Linking mutations to clinical significance).
7. **Visualisation:** maftools (R) (Oncoplots, mutation summaries, and lollipop plots).

---

## Key Difference from Germline Variant Calling

| Feature | Germline (GATK HaplotypeCaller) | Somatic / Cancer (GATK Mutect2) |
|---|---|---|
| Input samples | Single sample | Tumour AND matched normal |
| Variant type | Inherited SNPs and indels | Acquired somatic mutations |
| Allele frequency | ~50% or ~100% | Often low — 5% to 30% |
| Interpretation | ACMG classification | COSMIC / OncoKB actionability |
| Clinical use | Hereditary disease | Precision Cancer treatment |

---

## Knowledge Immersion Modules

- [x] **Module 1** — Infrastructure setup (WSL2, Miniconda, Tool Installation).
- [x] **Module 2** — Data curation and Reference Genome indexing.
- [ ] **Module 3** — Read Alignment logic and the impact of Reference Bias.
- [ ] **Module 4** — Mutation detection via GATK Mutect2.
- [ ] **Module 5** — Strategic filtering of somatic calls.
- [ ] **Module 6** — Clinical Annotation via Global Databases (COSMIC, OncoKB).
- [ ] **Module 7** — R-based genomic visualisation (maftools).
- [ ] **Module 8** — Clinical interpretation and summary of oncogenic significance.

---

## Background — Connecting to My Genomics Experience

My background in molecular biology involved end-to-end RNA-Seq analysis of 
chemosensory gene expression in *Glossina morsitans morsitans*, providing 
the wet-lab and bioinformatics foundation for this clinical oncology focus.

| Research NGS (RNA-Seq) | Clinical Cancer NGS (DNA-Somatic) |
|---|---|
| RNA expression changes | DNA somatic mutations |
| edgeR (differential expression) | Mutect2 (somatic calling) |
| FDR-corrected p-value | Variant allele frequency (VAF) |
| VectorBase annotation | COSMIC / OncoKB annotation |

---

## Author

**Joy Manyasi Kabaka**
MSc Biotechnology, Kenyatta University
Nairobi, Kenya

📧 jmanyasa@gmail.com
🔗 [RNA-Seq Publication — PLOS NTDs 2020](https://doi.org/10.1371/journal.pntd.0008341)

---

*This repository maps technical progress in cancer genomics literacy.
Started: May 2026.*
