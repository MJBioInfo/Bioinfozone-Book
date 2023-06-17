
# RNAseq Alignment

we install necesary packages 

```
#add repository channels to conda
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
#install STAR
conda install STAR

```

# Download and Store data in Bucket and link to folder of VM machine

Open SSH client 

go to the mountfolder (project folder)

create folder for storing reference genomes 
and RawReads folder


Get the Reference genome .fa and .gtf files and store in STARgenomefiles

# Reference genome

```
cd $HOME
#create folder for genome files
mkdir STARgenomefiles
cd STARgenomefiles

wget ftp://ftp.ensembl.org/pub/release-99/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
gunzip -k Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz


wget ftp://ftp.ensembl.org/pub/release-99/gtf/homo_sapiens/Homo_sapiens.GRCh38.99.gtf.gz
gunzip -k Homo_sapiens.GRCh38.99.gtf.gz

```

# Raw FastQ files

```
cd $HOME
mkdir myfastqfiles

# raw fastQ files

```

# Readcount 

```
cd $HOME
mkdir readcounts

```

# Analysis

## Index building

```
STAR --runThreadN 64 --runMode genomeGenerate --genomeDir $HOME/STARgenome --genomeFastaFiles $HOME/STARgenomefiles/Homo_sapiens.GRCh38.dna.primary_assembly.fa --sjdbGTFfile $HOME/STARgenomefiles/Homo_sapiens.GRCh38.99.gtf --sjdbOverhang 100

```


## Alignment by STAR

```

#sample-1.fastq:
STAR --runThreadN 96 --genomeDir $HOME/STARgenome --readFilesIn $HOME/myfastqfiles/sample-1.fastq --sjdbGTFfile $HOME/STARgenomefiles/Homo_sapiens.GRCh38.92.gtf --sjdbOverhang 100 --quantMode TranscriptomeSAM GeneCounts --outFileNamePrefix $HOME/readcounts/WTA-1 --genomeLoad LoadAndKeep


```
