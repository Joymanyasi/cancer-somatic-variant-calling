# 🧬 The Story of a Variant: A Detailed Look at the Kenyan TNBC Study (Saleh et al., 2021)

To understand my research, you have to understand the journey of a biological sample. This case study follows how researchers at the **Aga Khan University Hospital (Nairobi)** and their partners uncovered the "Kenyan Signature" in Triple-Negative Breast Cancer (TNBC).

### 1. The Biological Mystery
Imagine three women, one in **Nairobi**, one in **New York**, and one in **London**. All three are diagnosed with Triple-Negative Breast Cancer (TNBC). On the surface, their cancer looks identical under a microscope. But the woman in Nairobi often faces a more aggressive disease with fewer treatment options. 

**The Question:** Is the "code" inside the Nairobi tumour different?

### 2. The Technical Journey (The Pipeline)
To answer this, Saleh et al. didn't just look at the cells they looked at the **RNA (the messages the cells send)**. They moved through four technical stages:

#### **Stage A: Sequencing the "Messages"**
They took tumour samples from Kenyan women and used high-throughput sequencing (Illumina HiSeq) to read billions of tiny fragments of RNA. 
*   **The Literacy Link:** This is the same process I used in my **2020 Tsetse Fly research**. It turns complex biology into "Big Data."

#### **Stage B: Mapping to the "Global Anchor"**
They took those billions of Kenyan RNA fragments and "aligned" them to a **Reference Human Genome (GRCh38)**. 
*   **The Challenge:** Think of this like trying to fit pieces of a puzzle onto a pre-printed map. If the map (the Reference) is missing "landmarks" that only exist in Kenyan DNA, some of the most important pieces of the puzzle might be thrown away as "errors."

#### **Stage C: The "Subtraction" Math**
They compared the Kenyan "puzzle" against the "puzzles" of African American and Caucasian women from global databases (TCGA). 
*   **The Discovery:** They used statistical math (like **edgeR**) to "subtract" everything that was the same. What was left? **166 genes** that were "shouting" (highly expressed) in the Kenyan women but "whispering" in the others.

### 3. What the "Kenyan Signature" Actually Means
The researchers found that the Kenyan tumour wasn't just a "cancer cell" problem it was an **"Immune System"** conversation.
*   **The Finding:** Kenyan TNBC tumours were "hot"they were filled with immune cells (T-cells and Natural Killer cells). 
*   **Specific Genes:** They found high activity in genes like **CD2** and **KLRB1**. 
*   **Why it matters:** These genes are like "GPS coordinates" for the immune system. If a doctor in Kenya knows these genes are active, they might choose a completely different treatment (like immunotherapy) than a doctor in London.

### 4. The Critical Takeaway: Why "Cancer Variant" Research is Social Justice
If we only use a "Global Dictionary" (derived from Western cohorts) to define cancer:
1.  The **166 Kenyan genes** remain "Invisible" and unannotated.
2.  The Kenyan patient gets a **"Standard" treatment** that wasn't designed for her specific biology.
3.  The **Technical Pipeline** (GATK, BWA-MEM) becomes a tool of exclusion if it is not calibrated for African genomic diversity.

---
**Summary:** My "Cancer Variant" project is about mastering these technical tools (The Pipeline) so we can ensure that the biological truth of the Kenyan woman is never ignored again.

*Source: Saleh, M., et al. (2021). Comparative analysis of triple-negative breast cancer transcriptomics of Kenyan, African American and Caucasian Women. Translational Oncology, 14(14).*
