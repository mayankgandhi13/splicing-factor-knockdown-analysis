# Splicing-Factor Knockdown Analysis

Differential splicing analysis of public RNA-seq from splicing-factor knockdown experiments, using **rMATS** and **DEXSeq** run through the **nf-core/rnasplice** Nextflow pipeline.

> **Status:** In progress (started November 2026). Results will be added as each step is completed.

---

## Question

When a splicing factor is knocked down, which splicing events change, and do two different methods agree on them?

- **rMATS** detects and quantifies splicing *events* (skipped exons, retained introns, alternative 5'/3' splice sites, mutually exclusive exons) and tests for differences in percent spliced in (PSI).
- **DEXSeq** tests for differential *exon usage*, looking at exon-level counts rather than defined events.

Because the two methods model splicing differently, comparing their calls shows where results are robust and where they depend on the method used.

## Data

Public knockdown and control RNA-seq from the ENCODE project.

| Condition | Cell line | Replicates | ENCODE accession |
|-----------|-----------|------------|------------------|
| [Splicing factor] shRNA knockdown | K562 | 2 | [to be added] |
| Non-targeting control shRNA | K562 | 2 | [to be added] |

Reference: GRCh38 with GENCODE annotation.

## Pipeline

Analysis runs with [nf-core/rnasplice](https://nf-co.re/rnasplice), which handles QC, alignment, and differential splicing in one reproducible Nextflow workflow.

```bash
nextflow run nf-core/rnasplice \
  -profile docker \
  --input samplesheet.csv \
  --contrasts contrastsheet.csv \
  --genome GRCh38 \
  --outdir results \
  --rmats true \
  --dexseq_exon true
```

Check the [pipeline documentation](https://nf-co.re/rnasplice/parameters) for the exact parameter names in the version used. The pipeline version and all parameters are recorded in `results/pipeline_info/`.

## Repository structure

```
.
├── samplesheet.csv        # Sample metadata and FASTQ paths
├── contrastsheet.csv      # Knockdown vs control contrast
├── nextflow.config        # Run settings
├── analysis/              # R scripts for comparing rMATS and DEXSeq results
├── figures/               # Plots generated from the analysis
└── README.md
```

## Planned analysis

- [ ] Download FASTQ files and build the sample sheet
- [ ] Run nf-core/rnasplice with rMATS and DEXSeq
- [ ] Review QC (read quality, alignment rate, strandedness)
- [ ] Summarize significant rMATS events by type
- [ ] Summarize DEXSeq differential exon usage
- [ ] Map rMATS events and DEXSeq exons to shared genes and compare overlap
- [ ] Visualize top events (sashimi plots, PSI distributions)
- [ ] Write up where the two methods agree and disagree

## Results

To be added.

## Reproducing this analysis

1. Install [Nextflow](https://www.nextflow.io/) and Docker (or Singularity/Apptainer on HPC).
2. Clone this repository.
3. Download the FASTQ files listed in the Data table.
4. Update the paths in `samplesheet.csv`.
5. Run the command in the Pipeline section.

## Author

**Mayank Gandhi**
M.S. Bioinformatics, Northeastern University
[GitHub](https://github.com/mayankgandhi13) | [Portfolio](https://mayank-gandhi.vercel.app/)
