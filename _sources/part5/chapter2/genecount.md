
## Gene counts 

In this we are understanding how read ocunt is perfomed using HTseq-count and featurecounts 

We need following to efficiently calculate counts :

- Aligned file (BAM file)
- Annotation file (ref.gtf)



---

1. HTseq :

> htseq-count [options] <alignment_files> <gff_file > 


```
htseq-count -f bam \
            -r pos \
            -s no \
            -t gene \
            -i gene_id \
            --mode union \
            /path/to/aligned.bam \
            /path/to/annotation.gtf > /path/to/count_output.txt


```

Explanation of parameters:

-   -f bam: Specifies the input format as BAM.
-   -r pos: Strand-specific counting based on read alignment positions.
-    -s no: Indicates that the data is not strand-specific.
-    -t gene: Specifies the feature type to count (e.g., "gene").
-    -i gene_id: Specifies the attribute used as the feature identifier (e.g., "gene_id").
-    /path/to/aligned.bam: Path to the aligned BAM file.
-    /path/to/annotation.gtf: Path to the GTF annotation file.
-    /path/to/count_output.txt: Redirects the output to the specified text file.
-    --mode union: Specifies that overlapping features will be counted together (union mode).


---

2. Featurecounts : 

why use featurecounts ?

> For single end both featurecounts and HTseq-count are same. but for paired-end reads featurecounts is advanced :  For example, if two genes were found to both overlap with a reads pair fragment but one gene was found to overlap with only one read and the other with both reads from that fragment, featureCounts will assign that fragment to the gene overlapping with both reads. However, htseq-count will take this fragment as ambiguous and will not assign it to any gene.

> In HTseq-count , if in union mode : if read is overlap on 2 genes then it will not be counted (ambigous)
> 
> In HTseq-count , if in intersect mode :  if read partialy match gene and overhang outside gene , then it will not be counted

```
featureCounts -T 8 \
              -s 2 \
              -t gene \
              -g gene_id \
              -a /path/to/annotation.gtf \
              -o /path/to/count_output.txt \
              /path/to/aligned.bam


```

-   -T 8: Number of threads to use during counting.
-   -s 2: Specifies strand-specific counting. Use 0 for unstranded data, 1 for strand-specific data with the first read on  
     the  sense strand, and 2 for strand-specific data with the first read on the antisense strand.
-   -t gene: Specifies the feature type to count (e.g., "gene").
-   -g gene_id: Specifies the attribute used as the feature identifier (e.g., "gene_id").
-   -a /path/to/annotation.gtf: Path to the GTF annotation file.
-   -o /path/to/count_output.txt: Path to the output text file where counts will be saved.
-   /path/to/aligned.bam: Path to the aligned BAM file.