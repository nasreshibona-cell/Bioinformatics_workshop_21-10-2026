./scripts/trim.sh`.

### Software

**Command line (Ubuntu / WSL):**

``` bash
sudo apt update
sudo apt install fastqc cutadapt trim-galore rna-star multiqc

# Check installations
fastqc --version
cutadapt --version
trim_galore --version
STAR --version
multiqc --version
```

> If `multiqc` is not available through `apt`, install it with `pip install multiqc`.

**R / RStudio:**

``` r
install.packages(c("tidyverse", "BiocManager", "ggrepel", "pheatmap"))
BiocManager::install(c("rtracklayer", "DESeq2"))
```

### Make the scripts executable

``` bash
chmod +x scripts/*.sh
```

------------------------------------------------------------------------

## Step 1 – Download FASTQ files

**Script:** `Download-read_run-PRJNA714667-fastq_ftp-20261020-0707.sh`

### Get the sample information

1.  Open the ENA project page: <https://www.ebi.ac.uk/ena/browser/view/PRJNA714667>
2.  Show the columns **run_accession**, **experiment_accession** and **sample_title**.
3.  Click **TSV** to download the sample table and save it in `raw_data/`. You will need it in Step 7 to know which run is wild type and which is mutant.

### Get the download script

On the same page, select all runs and click **Get download script**. ENA generates a bash script with one `wget` command per file. There are 16 runs (`SRR13970433` – `SRR13970448`), each paired-end, giving **32 files**.

`wget -nc` ("no clobber") skips files that already exist, so the script is safe to re-run after an interruption.

### Run it

``` bash
cd raw_data
bash ../scripts/Download-read_run-PRJNA714667-fastq_ftp-20261020-0707.sh

# Check: should print 32
ls *.fastq.gz | wc -l
cd ..
```

<details>

<summary><b>Show the full download script</b></summary>

``` bash
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/040/SRR13970440/SRR13970440_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/041/SRR13970441/SRR13970441_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/038/SRR13970438/SRR13970438_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/044/SRR13970444/SRR13970444_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/047/SRR13970447/SRR13970447_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/035/SRR13970435/SRR13970435_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/034/SRR13970434/SRR13970434_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/046/SRR13970446/SRR13970446_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/035/SRR13970435/SRR13970435_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/036/SRR13970436/SRR13970436_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/038/SRR13970438/SRR13970438_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/033/SRR13970433/SRR13970433_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/045/SRR13970445/SRR13970445_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/048/SRR13970448/SRR13970448_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/040/SRR13970440/SRR13970440_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/043/SRR13970443/SRR13970443_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/039/SRR13970439/SRR13970439_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/047/SRR13970447/SRR13970447_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/037/SRR13970437/SRR13970437_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/042/SRR13970442/SRR13970442_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/043/SRR13970443/SRR13970443_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/048/SRR13970448/SRR13970448_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/036/SRR13970436/SRR13970436_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/044/SRR13970444/SRR13970444_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/039/SRR13970439/SRR13970439_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/042/SRR13970442/SRR13970442_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/041/SRR13970441/SRR13970441_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/045/SRR13970445/SRR13970445_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/046/SRR13970446/SRR13970446_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/033/SRR13970433/SRR13970433_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/034/SRR13970434/SRR13970434_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR139/037/SRR13970437/SRR13970437_1.fastq.gz
```

</details>

------------------------------------------------------------------------

## Step 2 – Download the reference genome

We use *E. coli* K-12 MG1655, assembly **ASM584v2** (`GCF_000005845.2`). Genome size, build and other details: <https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000005845.2/>

Only two files are needed: the genome sequence (FASTA) and the gene annotation (GTF).

``` bash
cd raw_data
BASE=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2

wget ${BASE}/GCF_000005845.2_ASM584v2_genomic.fna.gz
wget ${BASE}/GCF_000005845.2_ASM584v2_genomic.gtf.gz

# STAR needs uncompressed files
gunzip GCF_000005845.2_ASM584v2_genomic.fna.gz
gunzip GCF_000005845.2_ASM584v2_genomic.gtf.gz

# The scripts expect the GTF to be called genomic.gtf
mv GCF_000005845.2_ASM584v2_genomic.gtf genomic.gtf
cd ..
```

------------------------------------------------------------------------

## Step 3 – Quality control (FastQC + MultiQC)

**Script:** `fast_qc.sh`

Quality control is a crucial step before alignment. **FastQC** checks each FASTQ file. **MultiQC** combines all the reports into one HTML page so you can compare samples side by side.

### What to look for

| FastQC module | Good result / what it means |
|----|----|
| Per base sequence quality | Most bases above Phred 30; a drop at read ends means trimming is needed |
| Per sequence quality scores | Most reads are high quality overall |
| Per base sequence content | Early-cycle bias is common and should even out after trimming |
| Adapter content | Adapters present → they must be removed before alignment |
| Per sequence GC content | Follows the *E. coli* distribution (\~51 % GC); deviations suggest contamination |
| Sequence duplication levels | High duplication may reflect PCR bias or over-sequencing |

### Run it

``` bash
./scripts/fast_qc.sh
```

Then open `raw_data/fastqc_results/multiqc_report/multiqc_report.html` in a browser.

### Script

``` bash
#!/bin/bash

# === Define Project Directory ===
# raw_data/ sits next to this scripts/ folder (override by exporting PROJECT_ROOT)
PROJECT_ROOT="${PROJECT_ROOT:-$(cd "$(dirname "${BASH_SOURCE[0]}")/../raw_data" && pwd)}"

# === Move to Working Directory ===
cd "$PROJECT_ROOT" || { echo "Error: Cannot access $PROJECT_ROOT"; exit 1; }

# === Create Output Directory ===
mkdir -p fastqc_results

# === Run FastQC on all FASTQ files ===
fastqc *.fastq.gz -o fastqc_results

# === Move into the results folder ===
cd fastqc_results || exit

# === Run MultiQC ===
multiqc . -o multiqc_report

# === Print Completion Message ===
echo "FastQC and MultiQC analysis completed successfully."
echo "Results saved in: $PROJECT_ROOT/fastqc_results/multiqc_report"
```

> **Tip:** Add `--threads 4` to the `fastqc` line to process several files at once.

------------------------------------------------------------------------

## Step 4 – Trimming (Trim Galore)

**Script:** `trim.sh`

**Trim Galore** wraps cutadapt. For each read pair it:

- detects and removes adapter sequences,
- trims low-quality bases from the read ends,
- discards pairs where either read is shorter than **36 bp** after trimming (`--length 36`),
- runs FastQC on the trimmed reads (`--fastqc`), so you can compare before and after.

### Run it

``` bash
./scripts/trim.sh
```

### Outputs (in `raw_data/trimmed_reads/`)

| File                           | Content                        |
|--------------------------------|--------------------------------|
| `<sample>_1_val_1.fq.gz`       | Trimmed forward reads          |
| `<sample>_2_val_2.fq.gz`       | Trimmed reverse reads          |
| `*_trimming_report.txt`        | Trimming statistics            |
| `*_val_*_fastqc.html` / `.zip` | FastQC report on trimmed reads |

### Script

``` bash
#!/bin/bash

# raw_data/ sits next to this scripts/ folder (override by exporting PROJECT_ROOT)
PROJECT_ROOT="${PROJECT_ROOT:-$(cd "$(dirname "${BASH_SOURCE[0]}")/../raw_data" && pwd)}"

cd "$PROJECT_ROOT" || { echo "Error: Cannot access $PROJECT_ROOT"; exit 1; }

for sample in SRR139704{33..48}; do
  echo "Trimming $sample..."
  
  trim_galore --paired \
    ${sample}_1.fastq.gz ${sample}_2.fastq.gz \
    --output_dir trimmed_reads/ \
    --cores 4 --length 36 --fastqc

done
```

------------------------------------------------------------------------

## Step 5 – Indexing, alignment and gene counting (STAR)

**Script:** `ecoli_gene_quantification.sh`

### Genome indexing

Indexing prepares the reference genome so reads can be placed quickly and accurately. Instead of comparing each read to the genome base by base, aligners such as STAR, HISAT2 or BWA search the index. This makes alignment faster and lighter on memory while staying accurate in repetitive regions. Every downstream result depends on the quality of this step.

### Alignment and counting

With `--quantMode GeneCounts`, STAR aligns the reads and counts how many fall on each gene in the GTF, all in one step.

| Option | Meaning |
|----|----|
| `--sjdbOverhang 149` | Read length − 1 (for 150 bp reads) |
| `--readFilesCommand zcat` | Reads gzipped FASTQ directly |
| `--outSAMtype BAM SortedByCoordinate` | Writes a coordinate-sorted BAM file |
| `--quantMode GeneCounts` | Writes `ReadsPerGene.out.tab` per sample |

The FastQC and trimming blocks at the top of the script are commented out because Steps 3 and 4 already did them.

### Run it

``` bash
./scripts/ecoli_gene_quantification.sh

# Check the mapping rate of every sample (aim for > 80 %)
grep "Uniquely mapped reads %" raw_data/star_align/*Log.final.out
```

### Outputs per sample (in `raw_data/star_align/`)

| File | Content |
|----|----|
| `<sample>_Aligned.sortedByCoord.out.bam` | Aligned reads |
| `<sample>_Log.final.out` | Mapping statistics |
| `<sample>_SJ.out.tab` | Splice junctions (rare in bacteria) |
| `<sample>_ReadsPerGene.out.tab` | **Gene counts** |

### Understanding `ReadsPerGene.out.tab`

| Column | Content               | Use when the library is… |
|-------:|-----------------------|--------------------------|
|      1 | Gene ID (from GTF)    | —                        |
|      2 | Unstranded counts     | Unstranded               |
|      3 | Forward-strand counts | Forward-stranded         |
|      4 | Reverse-strand counts | Reverse-stranded         |

The first four rows (`N_unmapped`, `N_multimapping`, `N_noFeature`, `N_ambiguous`) are summary statistics, not genes.

> **Exercise:** Open one `ReadsPerGene.out.tab` and compare the totals of columns 3 and 4. If one is much bigger than the other, the library is stranded. If they are similar, it is unstranded.
>
> ``` bash
> tail -n +5 raw_data/star_align/SRR13970433_ReadsPerGene.out.tab | \
>   awk '{c2+=$2; c3+=$3; c4+=$4} END {print "unstranded:", c2, "forward:", c3, "reverse:", c4}'
> ```

### Script

``` bash
#!/bin/bash

# Set project root directory
# raw_data/ sits next to this scripts/ folder (override by exporting PROJECT_ROOT)
PROJECT_ROOT="${PROJECT_ROOT:-$(cd "$(dirname "${BASH_SOURCE[0]}")/../raw_data" && pwd)}"

# Define paths
GENOME_FASTA="$PROJECT_ROOT/GCF_000005845.2_ASM584v2_genomic.fna"
GTF_FILE="$PROJECT_ROOT/genomic.gtf"
THREADS=8
TRIMMED_DIR="$PROJECT_ROOT/trimmed_reads"
FASTQC_DIR="$PROJECT_ROOT/fastqc_results"
MULTIQC_DIR="$PROJECT_ROOT/multiqc_report"
STAR_INDEX_DIR="$PROJECT_ROOT/star_index"
STAR_ALIGN_DIR="$PROJECT_ROOT/star_align"

# Optional: Step 1 and 2 – FastQC + MultiQC (already done, commented out)
# mkdir -p "$FASTQC_DIR"
# fastqc *.fastq.gz -o "$FASTQC_DIR"
# cd "$FASTQC_DIR"
# multiqc . -o "$MULTIQC_DIR"
# cd "$PROJECT_ROOT"

# Step 3: Trimming (also commented out as already done)
# mkdir -p "$TRIMMED_DIR"
# for sample in SRR139704{33..48}; do
#   echo "Trimming $sample..."
#   trim_galore --paired \
#     ${sample}_1.fastq.gz ${sample}_2.fastq.gz \
#     --output_dir "$TRIMMED_DIR" \
#     --cores 4 --length 36 --fastqc
# done

# Step 4: STAR genome index generation
mkdir -p "$STAR_INDEX_DIR"

STAR --runThreadN "$THREADS" \
     --runMode genomeGenerate \
     --genomeDir "$STAR_INDEX_DIR" \
     --genomeFastaFiles "$GENOME_FASTA" \
     --sjdbGTFfile "$GTF_FILE" \
     --sjdbOverhang 149

# Step 5: STAR alignment
mkdir -p "$STAR_ALIGN_DIR"

cd "$TRIMMED_DIR" || { echo "Error: Cannot access $TRIMMED_DIR"; exit 1; }

for sample in $(ls *_1_val_1.fq.gz | sed 's/_1_val_1.fq.gz//' | sort -u); do
  READ1="${TRIMMED_DIR}/${sample}_1_val_1.fq.gz"
  READ2="${TRIMMED_DIR}/${sample}_2_val_2.fq.gz"

  if [[ -f "$READ1" && -f "$READ2" ]]; then
    echo "Aligning $sample..."
    STAR --runThreadN "$THREADS" \
         --genomeDir "$STAR_INDEX_DIR" \
         --readFilesIn "$READ1" "$READ2" \
         --readFilesCommand zcat \
         --outFileNamePrefix "$STAR_ALIGN_DIR/${sample}_" \
         --outSAMtype BAM SortedByCoordinate \
         --quantMode GeneCounts
  else
    echo "Skipping $sample — missing one or both trimmed FASTQ files." >&2
  fi
done

cd "$PROJECT_ROOT"
```

> **Recommended:** STAR suggests `--genomeSAindexNbases 10` for a genome as small as *E. coli*'s (\~4.6 Mb). Add it as an extra line in the `genomeGenerate` command to avoid warnings or crashes during indexing.

------------------------------------------------------------------------

## Step 6 – Merge gene counts (R)

**Script:** `megre data.R`

STAR writes one count file per sample. This script combines them into a single table, with genes as rows and samples as columns, and adds gene names from the GTF.

### What the script does

1.  Reads every `*_ReadsPerGene.out.tab` in `raw_data/star_align/`.
2.  Drops the 4 STAR summary rows and keeps **column 2 (unstranded counts)**.
3.  Merges all samples by gene ID and saves `merged_gene_counts.csv`.
4.  Imports the GTF and maps each gene ID to its gene name.
5.  Saves `merged_counts_annotated.csv` (gene names as row names) in the training folder.

### Before running

Open the script in RStudio and change `training_dir` to your own `training/` folder:

``` r
training_dir <- "/run/media/nasr/Crucial X9/bioinformatics_workshop/training"
# Windows + WSL example:
# training_dir <- "//wsl$/Ubuntu/home/<user>/training"
```

### Outputs

| File | Content |
|----|----|
| `raw_data/star_align/merged_gene_counts.csv` | Gene IDs + raw counts for every sample |
| `merged_counts_annotated.csv` | Same counts, gene names as row names |

### Script

``` r
library(tidyverse)
library(rtracklayer)

# Path to the training folder -- change this if the folder is moved
training_dir <- "/run/media/nasr/Crucial X9/bioinformatics_workshop/training"

setwd(file.path(training_dir, "raw_data", "star_align"))
gtf <- import(file.path(training_dir, "raw_data", "genomic.gtf"))

count_files <- list.files(pattern = "ReadsPerGene.out.tab$")
count_files
# Name samples based on filenames
sample_names <- gsub("_ReadsPerGene.out.tab", "", count_files)
# Function to read in just gene names and column 2 (unstranded counts)
read_counts <- function(file) {
  dat <- read.table(file, header = FALSE, sep = "\t", stringsAsFactors = FALSE)
  # Skip first 4 rows (STAR headers), then take only gene ID and column 2
  dat <- dat[-(1:4), c(1, 2)]
  colnames(dat) <- c("GeneID", file)
  return(dat)
}
read_counts
# Read all count files
count_list <- lapply(count_files, read_counts)
count_list
# Merge all data frames by "GeneID"
merged_counts <- Reduce(function(x, y) merge(x, y, by = "GeneID"), count_list)
# Rename columns to sample names
colnames(merged_counts) <- c("GeneID", sample_names)
# Save to CSV
write.csv(merged_counts, file = "merged_gene_counts.csv", row.names = FALSE)
# Optional: View the top of the table
head(merged_counts) 
dim(merged_counts)
# Load counts
counts <- read.csv("merged_gene_counts.csv")
dim(counts)

# Extract gene_id and gene_name mapping
gene_map <- unique(mcols(gtf)[,c("gene_id","gene")])
counts$GeneID <- as.character(counts$GeneID)

# Merge counts with annotation
counts_annot <- merge(counts, gene_map, by.x="GeneID", by.y="gene_id", all.x=TRUE)

# Rename gene column to "genes"
colnames(counts_annot)[colnames(counts_annot) == "gene"] <- "genes"

# Set "genes" as rownames
rownames(counts_annot) <- counts_annot$genes

# Drop GeneID and genes column from table
counts_annot <- counts_annot[, !(colnames(counts_annot) %in% c("GeneID", "genes"))]

setwd(training_dir)

# Save annotated table
write.csv(counts_annot, "merged_counts_annotated.csv")
dim(counts_annot)
```

> **Stranded library?** If the exercise in Step 5 showed the data are stranded, change `c(1, 2)` in `read_counts()` to `c(1, 3)` (forward) or `c(1, 4)` (reverse).

------------------------------------------------------------------------

## Step 7 – Differential expression (DESeq2)

**Script:** `DGE_e_coli.R`

This step compares the *slyA* mutant with the wild type using **DESeq2**. Inputs:

- `merged_counts_annotated.csv` from Step 6
- the ENA sample table from Step 1, which tells you which runs are **ECWT** and which are **ECMS**

Outputs: a table of differentially expressed genes and a volcano plot.

> *Script contents to be added.*

------------------------------------------------------------------------

## Troubleshooting {#troubleshooting}

| Problem | Likely cause | Fix |
|----|----|----|
| `Error: Cannot access .../raw_data` | Script not in `scripts/` next to `raw_data/` | Move it, or run with `PROJECT_ROOT=/path/to/raw_data` |
| STAR indexing warns or crashes | Genome too small for default index settings | Add `--genomeSAindexNbases 10` |
| STAR: `could not open genomeFastaFiles` / GTF | Reference still gzipped or GTF not renamed | `gunzip` the files and rename the GTF to `genomic.gtf` (Step 2) |
| Low mapping rate (\< 70 %) | Wrong reference, contamination or poor trimming | Recheck MultiQC; confirm the K-12 MG1655 reference |
| R: `duplicate 'row.names' are not allowed` | Some gene IDs map to the same or a missing gene name in the GTF | Keep only `gene` rows for the mapping (see below) |
| `ls: cannot access '*_1_val_1.fq.gz'` | Trimming not finished or wrong folder | Rerun `trim.sh`; check `raw_data/trimmed_reads/` |

**Safer gene-name mapping for Step 6:**

``` r
gene_map <- unique(as.data.frame(mcols(gtf[gtf$type == "gene"]))[, c("gene_id", "gene")])
gene_map$gene[is.na(gene_map$gene)] <- gene_map$gene_id[is.na(gene_map$gene)]
```
