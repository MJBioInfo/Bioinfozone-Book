## Differential Gene Expression :

> Main goal of differential expression tools is : Idntifying differential gene expression between conditions by reducing effect of unwanted variance (like variance by expremental conditions, systemic biases , batches etc..).



Lmma, edgeR, and DESeq2 are all popular R packages in R programming for the analysis of differential gene expression from RNA-seq data. They all serve a similar purpose, but they have differences in terms of their underlying statistical methods, assumptions, and use cases. The choice of which one to use depends on your specific research context and data characteristics.

---

| Package   | Advantages                                     | Use Cases and Data Characteristics                               |
|-----------|-----------------------------------------------|-----------------------------------------------------------------|
| limma     | - Robust with small sample sizes             | - Small sample sizes<br>- Stable variances                      |
|           | - Efficient statistical methodology          |                                                                 |
|           | - Works well with limited replicates         |                                                                 |
|-----------|-----------------------------------------------|-----------------------------------------------------------------|
| edgeR     | - Accommodates complex experimental designs | - Moderate to large sample sizes<br>- Complex experimental     |
|           | - Robust dispersion estimation              |   designs<br>- Moderate to high biological variability         |
|           | - Suitable for both small and large datasets|                                                                 |
|-----------|-----------------------------------------------|-----------------------------------------------------------------|
| DESeq2    | - Rigorous normalization                    | - Larger number of replicates<br>- Subtle changes in expression|
|           | - Detects subtle expression changes        |                                                                 |
|           | - Suitable for larger-scale studies        |                                                                 |


---




---

Here's a high-level overview of how DESeq2 works:

1. Normalization: RNA-seq data can have systematic biases due to various factors, such as differences in library size and gene length. DESeq2 applies a method called "size factor normalization" to account for these differences. This step ensures that the read counts for each gene are adjusted to a common scale, allowing valid comparisons between samples.

2. Statistical Modeling: DESeq2 uses a negative binomial distribution to model the variability in the count data. It estimates the dispersion parameter, which describes how the variance of the counts changes with the mean. This modeling approach is well-suited for count data, as it accounts for the inherent overdispersion often observed in RNA-seq data.

3. Differential Expression Analysis: DESeq2 performs hypothesis testing to identify genes that are differentially expressed between experimental conditions. It calculates a "log2 fold change" for each gene, which represents how much the expression of the gene changes between the conditions. It also computes a p-value to quantify the significance of the observed differences.

4. Multiple Testing Correction: Since you're usually testing thousands of genes simultaneously, there's a risk of observing false positives (genes that appear differentially expressed due to chance). DESeq2 applies multiple testing correction methods, such as the Benjamini-Hochberg procedure, to control the false discovery rate (FDR) and maintain a reasonable balance between true positives and false positives.

5. Results Interpretation: DESeq2 generates various outputs, including tables of differentially expressed genes, their fold changes, p-values, and adjusted p-values. Researchers typically focus on genes with significant changes (adjusted p-value < 0.05 or a chosen threshold) and substantial fold changes (e.g., greater than 2-fold or -2-fold) for further analysis and interpretation.

---

> Library Correction and Library composition Normalization



some some cases like only gene expressed in one type normal but not in other . then we have to Normalize by Library composition 

Suppose if we have Counts data as like below  . 
---

Original Count Values Table:

| Gene  | Cancer_1 | Cancer_2 | Normal_1 | Normal_2 |
|-------|----------|----------|----------|----------|
| Gene1 | 0        | 15       | 7        | 9        |
| Gene2 | 8        | 7        | 20       | 18       |
| Gene3 | 5        | 3        | 6        | 5        |



---

First we log transofrmed the data . In order to detect ouliers and Library composition and helps to remove from further downstream effect . 


---

Log2-Transformed Values Table:

| Gene  | log_Cancer_1 | log_Cancer_2 | log_Normal_1 | log_Normal_2 |
|-------|--------------|--------------|--------------|--------------|
| Gene1 | -Inf         | 3.906890596  | 2.807354922  | 3.169925001  |
| Gene2 | 3.000000000  | 2.807354922  | 4.321928095  | 4.169925001  |
| Gene3 | 2.321928095  | 1.584962501  | 2.584962501  | 2.321928095  |

---
Gene 1 is case of  - Library COmposition , we remove them in further normalization technique, to preserve cell type effect.

Average of each gene calculated (Which is called Geometric Mean as below)

---

Log2-Transformed Values Table with Geometric Mean (Corrected):

| Gene  | log_Cancer_1 | log_Cancer_2 | log_Normal_1 | log_Normal_2 | Geometric Mean |
|-------|--------------|--------------|--------------|--------------|----------------|
| Gene2 | 3.000000000  | 2.807354922  | 4.321928095  | 4.169925001  | 3.325056021    |
| Gene3 | 2.321928095  | 1.584962501  | 2.584962501  | 2.321928095  | 2.203186297    |


---

We get Library Composition Correction Table 

---
Library Composition Correction Table:

| Gene  | log_Cancer_1 | log_Cancer_2 | log_Normal_1 | log_Normal_2 | Geometric Mean |
|-------|--------------|--------------|--------------|--------------|----------------|
| Gene2 | 3.000000000  | 2.807354922  | 4.321928095  | 4.169925001  | 3.325056021    |
| Gene3 | 2.321928095  | 1.584962501  | 2.584962501  | 2.321928095  | 2.203186297    |

---

We devide each count with Median 

---
Devide each count with  with Median Row:

| Gene  | log_Cancer_1 | log_Cancer_2 | log_Normal_1 | log_Normal_2 | Geometric Mean |
|-------|--------------|--------------|--------------|--------------|----------------|
| Gene2 | 0.902227576  | 0.843225108  | 1.296601193  | 1.252445295  | 1.000000000    |
| Gene3 | 1.054735087  | 0.719199912  | 1.173406967  | 1.056871709  | 1.000000000    |
| Median| 0.978481332  | 0.781212510  | 1.235004080  | 1.154658502  | 1.000000000    |

---

We take Median value for each sample as below

---
Size Factors Table:

| Measurement  | log_Cancer_1 | log_Cancer_2 | log_Normal_1 | log_Normal_2 | Geometric Mean |
|--------------|--------------|--------------|--------------|--------------|----------------|
| Median       | 0.978481332  | 0.781212510  | 1.235004080  | 1.154658502  | 1.000000000    |
| Size Factor  | 2.657449966  | 2.182818389  | 3.444949732  | 3.176176431  | 1.000000000    |




Devide orginal counts value with Size factors to get Normalized counts table 

---

<pre>


<div style="display: flex; justify-content: space-between;">
    <div style="width: 48%;">
        Original Count Values Table:

        | Gene  | Cancer_1 | Cancer_2 | Normal_1 | Normal_2 |
        |-------|----------|----------|----------|----------|
        | Gene1 | 0        | 15       | 7        | 9        |
        | Gene2 | 8        | 7        | 20       | 18       |
        | Gene3 | 5        | 3        | 6        | 5        |
    </div>
    
    <div style="width: 48%;">
        Normalized Counts Table:

        | Gene  | Cancer_1 | Cancer_2 | Normal_1 | Normal_2 |
        |-------|----------|----------|----------|----------|
        | Gene1 | 0.000000 | 6.705593 | 2.098512 | 2.828428 |
        | Gene2 | 3.010626 | 3.210221 | 5.799378 | 5.670599 |
        | Gene3 | 1.882102 | 1.373534 | 1.744955 | 1.575154 |
    </div>
</div>


</pre>

---


