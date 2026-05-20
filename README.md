# ONT PCR Isoform Pipeline GUI

A browser-based GUI for running FLAIR-based isoform analysis on Oxford Nanopore PCR sequencing data.

## Features

- Add any number of samples
- Each sample supports 1 or more FASTQ.gz files (multi-lane → auto concatenated)
- Configurable genome, GTF, output path, conda env
- Toggle FLAIR flags: `--nvrna`, `--stringent`, `--check_splice`, `--longestORF`
- Standard mode (align → correct → collapse) or `flair transcriptome` mode
- Generates a complete, ready-to-run shell script
- Copy to clipboard or download as `.sh`

## Deploy to Render (free, ~2 minutes)

1. Fork or push this repo to your GitHub account
2. Go to [render.com](https://render.com) and sign up / log in
3. Click **New → Static Site**
4. Connect your GitHub repo
5. Render auto-detects `render.yaml` — just click **Deploy**
6. Your app is live at `https://ont-flair-pipeline.onrender.com` (or similar)

No build step, no backend, no cost.

## Local development

Just open `index.html` in any browser — no server needed.

```bash
open index.html
# or
python3 -m http.server 8080
```

## Pipeline steps generated

| Step | Tool | Description |
|------|------|-------------|
| 01 | `cat` / `cp` | Concatenate multi-lane FASTQ files |
| 02 | `flair align` | Map reads to genome |
| 03 | `flair correct` | Fix splice junctions with GTF |
| 04 | `flair collapse` | Collapse reads into isoforms |
| 05 | `flair combine` | Merge isoforms across samples |
| 06 | `flair quantify` | Quantify isoform expression |
| 07 | `predictProductivity` | Predict ORFs / NMD |
| 08 | `plot_isoform_usage` | Plot isoform usage for gene of interest |

## Requirements on your HPC

- [FLAIR 2.x](https://github.com/BrooksLab/flair) installed in a conda environment
- Gencode GRCh38 genome FASTA and GTF annotation
