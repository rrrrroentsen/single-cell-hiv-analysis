# single-cell-hiv-analysis

This tutorial describes how to create a custom Cell Ranger reference genome that includes both the human genome (GRCh38) and the HIV genome, followed by running a test analysis using 10x single-cell RNA sequencing (scRNA-seq) data.

## 1. Environment Setup
### 1.1 Download and Prepare Genome Files

Run the following commands to download and decompress the GRCh38 genome FASTA and GTF files from Ensembl:

```bash
# Download GRCh38 genome FASTA and GTF files
wget ftp://ftp.ensembl.org/pub/release-111/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
wget ftp://ftp.ensembl.org/pub/release-111/gtf/homo_sapiens/Homo_sapiens.GRCh38.111.gtf.gz

# Decompress the downloaded files
gzip -c -d Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz > Homo_sapiens.GRCh38.fa
gzip -c -d Homo_sapiens.GRCh38.111.gtf.gz > Homo_sapiens.GRCh38.111.gtf
```

### 1.2 HIV Genome Download

The HIV genome FASTA and annotation GTF files can be downloaded from the following link: 
https://drive.google.com/drive/folders/1izCR4YywcZrVogGyFpxoPGCNl0zSwlJQ?usp=drive_link


### 1.3 File Preparation

After downloading, ensure that the following files are ready:
HIV Genome FASTA: HIV.fa
HIV Annotation GTF: HIV_HXB2_LXS_version_3.3.gtf

### 1.4 Setting up Cell Ranger
Ensure that Cell Ranger is installed and properly set up by adding it to your environment path:

```bash
export PATH=~/cellranger-7.1.0:$PATH
which cellranger
```


## 2. Building the Custom Reference Genome
### 2.1 Preparing Files for Custom Reference

Make sure the following files are available in your working directory:

GRCh38 Genome FASTA: Homo_sapiens.GRCh38.fa

GRCh38 Annotation GTF: Homo_sapiens.GRCh38.111.gtf

HIV Genome FASTA: /path/to/HIV.fa

HIV Annotation GTF: /path/to/HIV_HXB2_LXS_version_3.3.gtf

### 2.2 Building the Reference

Change to your working directory and run the following command to build the custom reference:


```bash
cd /path/to/reference_folder/  
cellranger mkref \  
  --genome=GRCh38 \  
  --fasta=Homo_sapiens.GRCh38.fa \  
  --genes=Homo_sapiens.GRCh38.111.gtf \  
  --genome=HIV_LXS_3.3 \  
  --fasta=/path/to/HIV.fa \  
  --genes=/path/to/HIV_HXB2_LXS_version_3.3.gtf  
```

### 2.3 Example Output

The following is a sample of the expected output during the reference build process. The entire process may take approximately 1 hour:

```vbnet
Creating new reference folder at /path/to/reference_folder/GRCh38_and_HIV_LXS_3.3  
...done  
Writing genome FASTA file into reference folder...  
...done  
Indexing genome FASTA file...  
...done  
Writing genes GTF file into reference folder...  
...done  

Generating STAR genome index (may take over 8 core hours for a 3Gb genome)...  
May 09 11:12:34 ..... started STAR run  
May 09 11:12:34 ... starting to generate Genome files  
May 09 11:13:56 ... starting to sort Suffix Array. This may take a long time...  
May 09 12:17:46 ..... finished successfully  
...done.  

>>> Reference successfully created! <<<  
```



## 3. Conclusion
By following this tutorial, you can successfully create a custom Cell Ranger reference genome that incorporates both the human genome and the HIV genome. Additionally, you could replace the HIV genome with a patient-specific viral sequence to achieve more precise viral transcript analysis in 10x single-cell RNA sequencing data.
