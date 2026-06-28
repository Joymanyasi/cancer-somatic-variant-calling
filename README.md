
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

## 🔍 Conceptual Deep-Dive: The Logic of Somatic Calling

### What is a Somatic Variant?
Unlike germline variants (which are inherited and present in every cell), **somatic variants** are mutations that occur within a patient's lifetime in a specific tissue. In oncology, these mutations drive tumour growth. Identifying them is the core of **Precision Oncology**, allowing for targeted therapy and personalized treatment plans.

### The GATK "Gold Standard" (Mutect2)
The Broad Institute's **GATK (Genome Analysis Toolkit)** is the industry standard for high-accuracy variant discovery. For somatic research, the primary tool is **Mutect2**.

**The Core Methodology:**
1. **Matched-Normal Analysis:** The pipeline compares DNA from the patient's tumour against DNA from their own healthy "normal" tissue.
2. **Subtraction Logic:** Mutect2 "subtracts" the germline variants found in the normal sample. What remains are the **Somatic Candidates**.
3. **The "Panel of Normals" (PoN):** To reduce technical noise and sequencing artifacts, Mutect2 uses a PoN as an additional filter.

### Why GATK Literacy is Critical for AI Governance
As a critical social scientist, I focus on the **"Filtering Logic"** and **"Biological Assumptions"** of the GATK pipeline:
- **Reference Bias:** If the reference genome (**GRCh38**) is European-centric, we risk mis-aligning or "losing" variants unique to East African genomes during the initial alignment step.
- **PoN Bias:** If the **Panel of Normals** doesn't reflect African genomic diversity, the pipeline may incorrectly filter out important African-specific somatic variants as "noise."
- **Downstream Impact:** Since AI models are trained on the output of these pipelines, any "invisibility" at the GATK level is inherited and scaled by the resulting algorithms.

---




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

## Knowledge Immersion Modules & Resources

- [x] **Module 1: Infrastructure & Environment Control**  
  *Focus: Reproducible research environments using WSL2 and Conda.*  
  * [Conda User Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)
  
- [x] **Module 2: Data Curation & Reference Management**  
  *Focus: The GRCh38 human reference and its role as the "anchor" for clinical calls.*  
  * [NCBI Genome Reference Consortium](https://www.ncbi.nlm.nih.gov/grc/human)

- [ ] **Module 3: Alignment Logic & Reference Bias**  
  *Focus: BWA-MEM algorithm and how mapping choices affect variant detection.*  
  * [BWA-MEM Research Paper (Li, 2013)](https://arxiv.org/abs/1303.3997)

- [ ] **Module 4: Somatic Discovery with Mutect2**  
  *Focus: Bayesian logic for distinguishing low-frequency somatic mutations.*  
  * [GATK Mutect2 Technical Docs](https://gatk.broadinstitute.org/hc/en-us/articles/360037593851-Mutect2)

- [ ] **Module 5: Strategic Filtering & Artifact Removal**  
  *Focus: Identifying sequencing artifacts and orientation bias.*  
  * [Filtering Somatic Variants (Broad Institute)](https://gatk.broadinstitute.org/hc/en-us/articles/360035531132)

- [ ] **Module 6: Clinical Annotation & The "Knowledge Gap"**  
  *Focus: Analyzing the representation of African variants in global databases.*  
  * [OncoKB Precision Oncology Database](https://www.oncokb.org/) | [COSMIC v97](https://cancer.sanger.ac.uk/cosmic)

- [ ] **Module 7: Genomic Visualization in R**  
  *Focus: Summarizing mutational landscapes via oncoplots.*  
  * [maftools Documentation](https://bioconductor.org/packages/release/bioc/vignettes/maftools/inst/doc/maftools.html)

- [ ] **Module 8: Clinical Interpretation & Actionability**  
  *Focus: ESMO/ASCO tiers of actionability for targeted therapy.*  
  * [ESMO Scale for Clinical Actionability (ESCAT)](https://www.esmo.org/guidelines/esmo-scale-for-clinical-actionability-of-molecular-targets-escat)

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
