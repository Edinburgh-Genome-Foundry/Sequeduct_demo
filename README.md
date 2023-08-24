# Sequeduct demo

Demonstration data for the [Sequeduct](https://github.com/Edinburgh-Genome-Foundry/Sequeduct) pipeline.

#### View

Example files and results (`results_example`) can be browsed here or after downloading (cloning) the repository.

#### Run

The pipeline can also be run on the provided data. After installation of the pipeline as described on the [Sequeduct](https://github.com/Edinburgh-Genome-Foundry/Sequeduct) website, download (clone) the repository (click on the "<> Code" button on top of the page) and run the below commands.

All results are output in a newly created `results` directory.

## Preview

```bash
nextflow run edinburgh-genome-foundry/Sequeduct -r v0.3.0 -entry preview --fastq_dir='fastq_pass' \
    --sample_sheet='sample_sheet.csv' \
    -profile docker
```

The Preview pipeline runs a [NanoPlot](https://github.com/wdecoster/NanoPlot) analysis on the raw reads.
This is useful for getting an overview of our sequencing data. The results are saved in `results/dir1_preview` directory.

The pipeline requires a sample sheet that lists the selected barcodes (directories) that we want to analyse. This allows us to analyse a subset of the data, for example we have multiple projects.

## Analysis

```bash
nextflow run edinburgh-genome-foundry/Sequeduct -r v0.3.0 -entry analysis --fastq_dir='fastq_pass' \
    --reference_dir='genbank' \
    --sample_sheet='sample_sheet.csv' --projectname='EGF demo' -profile docker
```

The Analysis pipeline compares reads against the expected (designed) sequence. The results are saved in the `results/dir2_analysis` directory. Please see the publication, and the nextflow pipeline code and documentation for more details.

## Review

```bash
nextflow run edinburgh-genome-foundry/Sequeduct -r v0.3.0 -entry review --reference_dir='genbank' \
    --results_csv='results_reviewed.csv' \
    --projectname='EGF demo review' \
    --all_parts='parts_fasta/parts.fasta' \
    --assembly_plan='demo_assembly_plan.csv' \
    -profile docker
```

The Review pipeline aligns a user-defined list of sequences against the variant call consensus – or a *de novo* plasmid sequence assembled with Canu – and reports the alignments. This is useful for evaluating plasmids that are constructed from parts to clarify whether we have part or sample mix-ups, recombination events or overhang misannealing.

This pipeline can only be run after running the Analysis pipeline as it uses the generated files. The results are saved in `results/dir3_review` directory.

## Assembly

```bash
nextflow run edinburgh-genome-foundry/Sequeduct -r v0.3.0 -entry assembly --fastq_dir='fastq_pass' \
    --assembly_sheet='de_novo_assembly_sheet.csv' \
    -profile docker
```

A standalone Assembly pipeline creates *de novo* assembly sequences, without any reference files. The results are saved in `results/dir4_assembly` directory.

## Notes

Please use the [Sequeduct](https://github.com/Edinburgh-Genome-Foundry/Sequeduct) project's page to file any issues or comments.

Copyright 2023 Edinburgh Genome Foundry, University of Edinburgh
