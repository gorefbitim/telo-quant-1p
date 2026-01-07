# HG002 Chromosome 1p Telomere Quantification

This project provides an efficient, single-molecule approach to quantifying telomere lengths on the **1p arm** of the HG002 human genome. By leveraging **Oxford Nanopore Technologies (ONT)** ultra-long reads, we traverse repetitive regions that are typically "invisible" to short-read sequencing.

## The Power of ONT for Telomere Biology
Telomeres and subtelomeres are notoriously difficult to resolve due to high repeat density. Traditional methods often fail to anchor these sequences to specific chromosomes.

Using ONT data allows us to:
* **Anchor:** Use unique subtelomeric sequences to verify the read belongs to Chromosome 1p.
* **Traverse:** Read through the entire repetitive array in a single continuous molecule.
* **Quantify:** Measure the "Perfect" canonical core length ($TTAGGG_n$) with single-molecule resolution.

## Methodology
The analysis utilizes a direct string-matching algorithm to identify canonical human telomere hexamers:
* **Forward Motif:** `TTAGGG`
* **Reverse Complement:** `CCCTAA`

**Formula:** $L = (Count_{fwd} + Count_{rev}) \times 6$

This establishes a conservative baseline for the **Canonical Telomere Length**, effectively filtering out Telomere Variant Repeats (TVRs) and sequencing artifacts to find the "perfect" core.

## Data Source & Requirements
The analysis is performed on the **HG002** (AJ Son) benchmark dataset. While the full ONT dataset is several terabytes, this analysis uses a filtered extract of reads anchored to the 1p arm.

### Download Sample Data
You can fetch the specific test file used in this analysis directly from the `telogator2` reference repository:

```bash
# Download to your data directory and decompress
wget https://github.com/zstephens/telogator2/raw/main/test_data/hg002-ont-1p.fa.gz -P data/
gunzip data/hg002-ont-1p.fa.gz
```

### Environment
* **Python:** 3.10.9
* **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `biopython`

## Citation
This work is inspired by the methodological framework of **Telogator2**.

> **Stephens, T. G., & Kocher, J. P. (2024).** *Telogator2: Allele-specific analysis of telomeres and subtelomeres using long-read sequencing.* Bioinformatics. [doi:10.1093/bioinformatics/btad723](https://doi.org/10.1093/bioinformatics/btad723)
