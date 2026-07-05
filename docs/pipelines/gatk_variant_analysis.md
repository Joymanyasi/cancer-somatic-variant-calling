# GATK Pipeline for Kenyan TNBC Variant Analysis  
*Part of the “Cancer Variant” project on algorithmic inequity in biomedical AI*

---

## 1. Why This Pipeline Matters

This repository documents my use of the **GATK (Genome Analysis Toolkit) pipeline** to study **variants in Triple-Negative Breast Cancer (TNBC) in Kenyan women**, inspired by the Saleh et al. (2021) study on the “Kenyan Signature” in TNBC transcriptomics.

The core problem:

- Standard genomic pipelines and reference genomes are largely built on **non‑African data**.
- When we push Kenyan tumour samples through these pipelines “out of the box”, **Kenyan‑specific signals can be discarded as noise**.
- This has direct consequences for:
  - Which variants we see and annotate,
  - Which treatment options look viable,
  - How future AI tools for oncology are trained and evaluated.

This project treats the GATK workflow not just as a technical pipeline, but as a **site of social justice**: a place where we can either **erase** or **preserve** the biological truth of East African women.

---

## 2. Conceptual Anchor: From the “Kenyan Signature” to Kenyan Variant Profiles

Saleh et al. (2021) sequenced TNBC tumours from Kenyan women and compared them to African American and Caucasian women. Using RNA‑seq and differential expression analysis (e.g., edgeR), they:

- Identified **166 genes** that were highly expressed in Kenyan tumours but low in others.
- Showed that Kenyan TNBC tumours appeared **immunologically “hot”**, with strong immune cell signatures (e.g., **CD2**, **KLRB1**).
- Demonstrated that **population‑specific biology matters** for treatment choices, including potential responsiveness to immunotherapy.

My **Cancer Variant** project extends this logic to the **variant level**:

> If Kenyan TNBC has a distinct expression “signature”, what does the **underlying variant landscape** look like and how does a standard GATK pipeline handle it?

---

## 3. Overview of the GATK‑Based Workflow

This repository focuses on a **GATK‑style variant calling pipeline**, conceptually aligned with Best Practices, but viewed through the lens of **African genomic diversity and algorithmic inequity**.

### High‑Level Stages

1. **Input & QC**  
   - Start from raw sequencing reads (DNA or RNA) from Kenyan TNBC tumours.
   - Perform quality control and trimming to remove adapters and low‑quality bases.

2. **Alignment to Reference**  
   - Align reads to the human reference genome (e.g., GRCh38) using **BWA‑MEM** or similar.
   - This step is where Kenyan‑specific sequences can fail to map if the reference does not adequately represent African diversity.

3. **Preprocessing (GATK)**  
   - Mark duplicates, perform base quality score recalibration (BQSR), and other standard clean‑up steps.
   - These procedures are typically calibrated on non‑African variant sets.

4. **Variant Calling (GATK)**  
   - Call variants using tools such as **HaplotypeCaller** (germline) or **Mutect2** (somatic).
   - Apply filters to distinguish real variants from artefacts.

5. **Comparison & Interpretation**  
   - Compare Kenyan variant calls to global resources (e.g., TCGA TNBC cohorts).
   - Look for **variants that are enriched or unique** in Kenyan samples, in analogy with the 166‑gene “Kenyan Signature”.

The project goal is to use and adapt each stage so that **African‑specific variants are preserved, not filtered out.**

---

## 4. Stage‑by‑Stage Narrative

### 4.1 From Tumour to Reads: Turning Biology into Data

- Tumour samples from Kenyan TNBC patients are sequenced on high‑throughput platforms (similar technology was used in my earlier Tsetse Fly RNA‑seq work).
- Biology becomes **Big Data**: millions to billions of short reads.
- At this stage, the main concern is **basic data quality**; the equity questions intensify once we start aligning to reference genomes and calling variants.

---

### 4.2 Alignment: Fitting Kenyan Reads to a Non‑Kenyan Map

**Analogy:**  
Aligning Kenyan reads to the human reference genome is like trying to fit pieces of a Kenyan puzzle onto a **world map drawn mostly from European landmarks**.

- Tool: BWA‑MEM (or similar aligner).
- Reference: GRCh38, which has limited direct representation of East African genomes.
- Risk:
  - Reads containing Kenyan‑specific insertions, structural variants, or highly divergent haplotypes may:
    - Fail to align,
    - Map poorly,
    - Be flagged as low quality and discarded.

In my narrative:

> This is the first point where the pipeline can silently push Kenyan biology off the map.

---

### 4.3 Preprocessing: Cleaning vs. Silencing

Standard GATK preprocessing includes:

- **Marking PCR duplicates**  
  - Necessary for removing amplification artefacts.
- **Base Quality Score Recalibration (BQSR)**  
  - Uses known variant sites to adjust base quality scores.
- **RNA‑specific steps** (if working from RNA‑seq): splitting reads across exon–intron boundaries.

Equity concern:

- BQSR models and known variant sets are mostly built from **non‑African** data.
- True African variants may be mis‑modelled as errors, which:
  - Decreases their quality scores,
  - Makes them less likely to be called as real variants downstream.

In this project, I treat BQSR and related steps as **critical levers**: how we configure and interpret them affects whether African variation survives to the final VCF.

---

### 4.4 Variant Calling: Who Decides What Counts as “Real”?

Variant calling is where the pipeline formally decides:

- Which positions differ from the reference (SNPs, indels),
- How confident we are that these differences are real.

Typical GATK‑style commands (conceptually):

- **HaplotypeCaller** for germline variants.  
- **Mutect2** for somatic tumour‑normal variant calling.

Equity concern:

- Filtering and confidence thresholds are often tuned using data where **African populations are under‑represented**.
- Variants that:
  - Are rare globally,
  - But common or important in East African populations,
  can be misclassified as errors or low‑confidence calls.

In my research narrative:

> I treat the variant caller not as a black box, but as a **negotiation space**, where we ask: “Real for whom? Under which assumptions? Calibrated on which bodies?”

---

### 4.5 Comparison & Subtraction: Toward a “Kenyan Variant Profile”

Inspired by the Saleh et al. transcriptomic comparison, the variant‑level analysis follows a similar logic:

1. **Catalogue** variants in Kenyan TNBC samples using the GATK pipeline.  
2. **Compare** against:
   - TNBC variant sets from global databases such as TCGA (where available),
   - Where possible, public African variant resources.
3. **Subtract**:
   - Focus on variants that are:
     - Present and relatively common in Kenyan TNBC,
     - Rare or absent in non‑African TNBC cohorts.

The long‑term goal is to build a **“Kenyan Variant Profile”** that complements the “Kenyan Signature” at the gene‑expression level:

- Highlighting immune‑related variants,
- Identifying variants potentially linked to drug response or resistance,
- Providing inputs for more equitable AI models and clinical decision tools.

---

## 5. Justice Lens: From Pipeline Defaults to Algorithmic Inequity

This GATK pipeline is embedded in a broader research agenda on **algorithmic inequity in biomedical AI for East African women’s health**:

- If **African variants are under‑detected or poorly annotated** at the pipeline stage,
  - Then downstream AI models trained on these incomplete datasets will be biased.
  - Clinical decision support systems will systematically underperform for Kenyan women with TNBC.
- By critically engaging with each GATK step, I treat variant calling as:
  - A **technical task** (getting accurate calls), and
  - A **political–ethical task** (ensuring that East African bodies are not rendered invisible in “global” oncology).

---

## 6. What This Repository Represents

This GitHub repository is:

- A **documentation space** for how I conceptualise and adapt a GATK‑based pipeline for Kenyan TNBC data.
- A bridge between:
  - **Hands‑on bioinformatics** (alignment, preprocessing, variant calling),
  - **Critical social science** (algorithmic inequity, data justice, Ubuntu‑informed governance),
  - And **clinical relevance** (treatment options shaped by population‑specific biology).

In one line:

> The GATK pipeline here is not just about calling variants it is about ensuring that the molecular realities of Kenyan women with TNBC are technically visible, analytically respected, and ethically centred in the future of AI‑enabled cancer care.

---
