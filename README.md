# Cancer Somatic Variant Calling Pipeline

![Status](https://img.shields.io/badge/Status-In%20Progress-blue)
![Platform](https://img.shields.io/badge/Platform-GATK%20Mutect2-orange)
![Data](https://img.shields.io/badge/Data-TCGA%20Public-green)

A self-directed portfolio project implementing a clinical-grade somatic 
variant calling pipeline on publicly available cancer sequencing data.

Built by a molecular biologist with first-author RNA-Seq experience 
(PLOS NTDs, 2020), actively expanding into clinical cancer genomics.

---

## Motivation

Cancer genomics is one of the fastest-growing applications of clinical 
NGS globally. Somatic variant detection identifying mutations acquired 
by tumour cells  is central to precision oncology, targeted therapy 
selection, and diagnostic reporting in clinical laboratories.

This project bridges my existing NGS research skills toward clinical 
cancer genomics competency, following the GATK Best Practices somatic 
short variant discovery pipeline developed by the Broad Institute.

---

## Dataset

| Detail | Information |
|---|---|
| Sample | HCC1143 breast cancer cell line |
| Type | Tumour + matched normal pair |
| Source | Broad Institute GATK tutorial (publicly available) |
| Reference genome | GRCh38 / hg38 |
| Sequencing type | Whole exome sequencing (WES) |
| Data access | No patient data — open access tutorial dataset |

---

## Pipeline Overview
Tumour FASTQ  +  Normal FASTQ
│
▼
Alignment — BWA-MEM → GRCh38
│
▼
BAM processing — SAMtools + Picard
(sort, index, mark duplicates)
│
▼
Base Quality Score Recalibration — GATK BQSR
│
▼
Somatic variant calling — GATK Mutect2
(tumour-with-matched-normal mode)
│
▼
Variant filtering — GATK FilterMutectCalls
│
▼
Variant annotation — ANNOVAR + COSMIC + OncoKB
│
▼
Visualisation — maftools (R)
(mutation summary, oncoplot, lollipop plots)
│
▼
Clinical interpretation
(oncogenic significance, actionability tier)

---

## Tools and Software

| Tool | Purpose | Version |
|---|---|---|
| BWA-MEM | Read alignment | 0.7.17 |
| SAMtools | BAM processing | 1.17 |
| Picard | Duplicate marking | 3.0 |
| GATK Mutect2 | Somatic variant calling | 4.4 |
| ANNOVAR | Variant annotation | Latest |
| COSMIC | Cancer mutation database | v97 |
| OncoKB | Clinical actionability | Latest |
| maftools | R visualisation | 2.16 |
| IGV | Variant visualisation | 2.16 |

---

## Key Difference from Germline Variant Calling

| Feature | Germline (GATK HaplotypeCaller) | Somatic / Cancer (GATK Mutect2) |
|---|---|---|
| Input samples | Single sample | Tumour AND matched normal |
| Variant type | Inherited SNPs and indels | Acquired somatic mutations |
| Allele frequency | ~50% or ~100% | Often low — 5% to 30% |
| Filtering | VQSR | FilterMutectCalls |
| Interpretation | ACMG classification | COSMIC / OncoKB actionability |
| Clinical use | Hereditary disease | Cancer diagnosis and treatment |

---

## Progress Tracker

- [ ] Week 1 — WSL2 setup, Miniconda, tool installation
- [ ] Week 2 — Download dataset, index reference genome
- [ ] Week 3 — Align tumour and normal BAMs using BWA-MEM
- [ ] Week 4 — Run GATK Mutect2 somatic variant calling
- [ ] Week 5 — Filter variants with FilterMutectCalls
- [ ] Week 6 — Annotate with ANNOVAR, COSMIC, OncoKB
- [ ] Week 7 — Visualise with maftools in R
- [ ] Week 8 — Interpret results and write clinical summary

---


---

## Background — Connecting to My Research Experience

My previous NGS work involved end-to-end RNA-Seq analysis of 
chemosensory gene expression in *Glossina morsitans morsitans* 
tsetse fly, including:

- Total RNA extraction using TRIzol (Invitrogen)
- Library preparation using TruSeq RNA Sample Prep Kit (Illumina)
- Sequencing on Illumina HiSeq 2500 at Yale YCGA
- Bioinformatics analysis: FastQC, CLC Genomics Workbench v10, edgeR
- Data deposited to NCBI SRA: PRJNA343267 and PRJNA343269

This cancer genomics project extends those skills from:

| Research NGS | Clinical Cancer NGS |
|---|---|
| RNA expression changes | DNA somatic mutations |
| edgeR (differential expression) | Mutect2 (somatic calling) |
| FDR-corrected p-value | Variant allele frequency (VAF) |
| Gene ontology enrichment | Oncogenic pathway analysis |
| VectorBase annotation | COSMIC / OncoKB annotation |

---

## Resources Being Used

- GATK Somatic Best Practices:
  https://gatk.broadinstitute.org/hc/en-us/articles/360035894731
- COSMIC cancer mutation database:
  https://cancer.sanger.ac.uk/cosmic
- OncoKB precision oncology database:
  https://www.oncokb.org
- maftools R package (Mayakonda et al., 2018):
  https://bioconductor.org/packages/maftools
- Illumina iSchool free NGS training:
  https://www.illumina.com/services/training.html

---

## Author

**Joy Manyasi Kabaka**
MSc Biotechnology, Kenyatta University
BSc Biochemistry & Molecular Biology, JKUAT
Nairobi, Kenya

📧 jmanyasa@gmail.com
🔗 [RNA-Seq Publication — PLOS NTDs 2020](https://doi.org/10.1371/journal.pntd.0008341)
🔗 [NCBI SRA — PRJNA343267](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA343267)
🔗 [NCBI SRA — PRJNA343269](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA343269)

---

## Citation — RNA-Seq Background Work

Kabaka JM, Wachira BM, Mang'era CM, Rono MK, Hassanali A, Okoth SO,
Oduol VO, Macharia RW, Murilla GA, Mireji PO (2020). Expansions of
chemosensory gene orthologs among selected tsetse fly species and their
expressions in *Glossina morsitans morsitans* tsetse fly.
*PLoS Negl Trop Dis* 14(6): e0008341.
https://doi.org/10.1371/journal.pntd.0008341

---

*This repository is actively updated weekly as the project progresses.
Started: May 2026.*
