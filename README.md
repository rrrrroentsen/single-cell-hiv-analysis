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
