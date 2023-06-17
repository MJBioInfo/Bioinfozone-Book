
# Introduction

There are many cloud computing platforms available to work on Next Generation Sequemcing analysis like Amazon's AWS , Google cloud computing, Microsoft Azure. 

In this chapter we are going to explain how to use Google cloud platform to analyse Next generation sequencing .

Here we are going to get read counts data from RawReads / FastQ data .

Suppose if you wanted to do RNAseq analysis you need high performing computers (More cores, Threads, high RAM). 
if you don't have access to such high performing computers then there is an option for Google cloud for a reasonable price (with Free trail)

## Google Cloud Computing (GCP) 

In Google cloud we are using free trail , which Gives $300 / 3 months credit , which is sufficient to do some Data analysis , including high RAM sequence analysis.

We are showing here RNA sequence Alignment using STAR , which runs on High RAM Machines ( More than 32 GB )

Below are steps to achive RNAseq alignment using GCP ; Briefly :

1) Selecting Operating system (we use Linux : Ubuntu flavour)

2) Custom selection of Resources according to alignment algorithm STAR (High RAM / Threads)

3) Creating Conda Environment

4) Installing required Packges 

5) Linking downloaded data with Bucket and VM machine 

6) Running STAR alignment on FASTQ reads to get Gene count 



# Setup GCP

# RNA seq Analysis 

## Alignment