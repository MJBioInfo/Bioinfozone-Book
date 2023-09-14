## Sequence Alignment Methods

---
| Feature                  | BWA                  | Bowtie               | STAR                 | HISAT                | Salmon               | Minimap2             |
|--------------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|
| Alignment Type           | DNA and Variant Calling | Short Reads         | RNA-Seq (Spliced)   | RNA-Seq (Spliced)   | RNA-Seq (Transcript) | DNA and RNA          |
| Algorithm                | Burrows-Wheeler Transform | Burrows-Wheeler Transform | 2-Step (Genome & Junction) | Hierarchical Indexing | Selective Alignment  | Minimizer-based Align |
| Alignment Purpose        | Whole Genome, Variant Calling | ChIP-seq, Small Reads | Gene Expression, Alternative Splicing | Gene Expression, Alternative Splicing | Transcript Quantification | DNA and RNA Sequencing |
| Read Length              | Short to Long        | Short                | Short to Long        | Short to Long        | Short to Long        | Short to Long        |
| Alignment Speed          | Moderate to Fast     | Fast                 | Fast and Accurate    | Fast and Accurate    | Very Fast            | Very Fast            |
| Splice Junctions         | Not Focused          | Not Considered      | Detected and Known   | Detected and Known   | Not Considered      | Not Considered      |
| Application              | Genomic Variants, SNP Calling | Mapping Small Reads | Gene Expression, Alternative Splicing | Gene Expression, Alternative Splicing | Transcript Quantification | Genomic and Transcript |
| Novel Junctions          | Not Emphasized       | Not Emphasized      | Emphasized           | Emphasized           | Not Emphasized      | Not Emphasized      |
| Specialized for          | DNA Sequencing       | Short Reads          | RNA-Seq with Splicing | RNA-Seq with Splicing | RNA-Seq Transcript  | DNA and RNA Sequencing |
| Algorithm Focus          | Global and Local Alignment | Global Alignment | Spliced Alignment    | Spliced Alignment    | Alignment and EM    | Minimizer-based Align |
| Multiple Alignments      | Yes                  | Yes                  | Yes                  | Yes                  | Yes                  | Yes                  |
| Transcript Quantification| No                   | No                   | No                   | No                   | Yes                  | No                   |
                |
---







---

| Alignment Tool   | Advantages                                            | Disadvantages                                                                                                      |
|------------------|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| BWA              | - Accurate alignments for both short and long reads. | - May have higher memory usage for longer reads and larger genomes.                                                |
|                  | - Suitable for DNA sequencing and variant calling.   | - May not be the fastest option for very large genomes or highly repetitive regions.                              |
| Bowtie           | - Very fast for short read alignments.               | - Only supports short read alignments and is not designed for spliced alignments.                                 |
|                  | - Efficient for small genomes and repetitive regions.| - May not provide as accurate alignments in the presence of structural variations.                                |
| STAR             | - Accurate spliced alignments for RNA-Seq data.     | - Consumes significant memory, especially for indexing, and may require substantial resources for large datasets. |
|                  | - Identifies known and novel splice junctions.      | - Initial indexing process can be time-consuming and resource-intensive.                                           |
| HISAT            | - Efficiently handles spliced alignments in RNA-Seq. | - May not be as memory-efficient as other tools.                                                                   |
|                  | - Detects and aligns across known and novel junctions.| - Alignment speed can vary based on dataset characteristics.                                                        |
| Salmon           | - Designed for transcript quantification.           | - Designed specifically for transcript quantification and may not be suitable for other types of alignments.      |
|                  | - Rapid and accurate quantification for RNA-Seq.    | - May not provide accurate gene-level quantification if multiple isoforms are not well-distinguished.            |
| Minimap2         | - Very fast and efficient for various data types.   | - May not perform as well on extremely long reads or in regions with high complexity.                             |
|                  | - Suitable for both DNA and RNA sequencing.         | - May have limitations in aligning very short reads due to its minimizer-based strategy.                         |

---





> In Every alignment , we first try to Index reference genome to make algorithm fast and then alignment 



1. BWA :

Index Building:

```
bwa index  /path/to/reference_genome.fasta  -p /path/to/index_prefix

```

2. Bowtie :



```
bowtie2-build /path/to/reference_genome.fasta /path/to/index_prefix

```

3. HISAT2:



```
hisat2-build  /path/to/reference_genome.fasta /path/to/index_prefix  

```

4. STAR :



```
STAR --runMode genomeGenerate \
     --genomeDir /path/to/genome_index \
     --genomeFastaFiles /path/to/reference_genome.fasta

```

5. Salmon :

```
salmon index -t /path/to/transcriptome.fasta -i /path/to/index_name

```

6. Minmap2 :

```
minimap2  /path/to/reference_genome.fasta  -d /path/to/index.mmi

```




Alignment:


1. BWA :

```
bwa mem -t 8 \
        /path/to/reference_genome.fasta \
        /path/to/read1.fq /path/to/read2.fq \
        > /path/to/aligned.sam


```



2. Bowtie :


```
bowtie2 -p 8 \
        -x /path/to/index_prefix \
        -1 /path/to/read1.fq \
        -2 /path/to/read2.fq \
        -S /path/to/aligned.sam

```

3. HISAT2:


```
hisat2 -p 8 \
       -x /path/to/index_prefix \
       -1 /path/to/read1.fq \
       -2 /path/to/read2.fq \
       -S /path/to/aligned.sam

```

4. STAR :

```
STAR --genomeDir /path/to/genome_index \
     --readFilesIn /path/to/read1.fq /path/to/read2.fq \
     --outFileNamePrefix /path/to/aligned_ \
     --runThreadN 8

```

5. Salmon :

```
salmon quant -i /path/to/index_name \
             -l A \
             -1 /path/to/read1.fq \
             -2 /path/to/read2.fq \
             -o /path/to/output_directory \
             -p 8

```

6. minmap2 :

```
minimap2 -t 8 \
         -a /path/to/index.mmi \
         /path/to/read1.fq /path/to/read2.fq \
         > /path/to/aligned.sam

```

---





