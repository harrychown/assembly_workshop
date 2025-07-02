# Genome assembly workshop

This genome assembly workshop will provide you with the skills to correctly assembly and annotate a fungal genome from short-read sequencing data.
In this workshop you will learn how to do the following:

- Quality-control sequencing runs
- Trim and filter sequencing reads
- Remove potential contamination
- Assemble the mitogenome
- Assemble the nuclear genome
- Polish the nuclear genome
- Perform quality-control on the nuclear genome
- Annotate the nuclear genome, either *de novo* or reference based

The pipeline and tools provided may become redundant over time, therefore this tutorial will not be static and may change to reflect improvements in the field and updates in software. Additionally, the tutorial may be built upon with new features being added. This workshop and subsequent genome assemblies have not been benchmarked and may not be the "gold-standard" for the genome you want to create with the data that you have. Please feel free to reach out if you have any queries. 

This workshop has been developed for Matthew Fisher's lab group based in Imperial College London. Therefore, tools have been selected that run on internal HPC machines and may not reflect the tools that are available for yourself. We would like to apologise for this in advance if you have difficulty in either accessing these tools or the computational run-time required for using these tools.


## Requirements

### Software

The majority of the software needed will be downloaded and install via Conda in individual environments. Environments have been developed and saved as YAML files in `envs/`. 

- Conda
- Internet connection
- FastQC v0.12.1
- fastp v0.24.0
- GetOrganelle v1.7.7.1
- BWA v0.7.18-r1243-dirty
- samtools v1.18
- QualiMap v2.2.2-dev
- bedtools v2.31.1
- SPAdes v4.0.0
- AAFTF v0.4.1
- Pilon v1.24
- RagTag v2.1.0


### Conda installed software/environments

- `biomaRt`
- `seqinr`
- `optparse`

You can install them using the following commands in R:

```r
install.packages("optparse")
install.packages("seqinr")
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("biomaRt")
```

## Installation


pep2geneID can be "installed" by simply downloading the script ```pep2geneID.R``` .


## Workshop data

Data for this workshop can be found in `data/`. Example sequencing data consists of *Aspergillus fumigatus* sequencing reads (BioProject:PRJEB1497, Run:ERR232427) which correctly mapped to chromosome 1 of the latest CEA10 genome (https://www.nature.com/articles/s41467-022-32924-7#data-availability) and the mitochondrial genome (NC_017016.1). A pangenome reference proteome was obtained from https://github.com/harrychown/asp_pan (https://www.nature.com/articles/s41564-022-01091-2). Alongside the latest CEA10 genome, an additional reference genome has also been provided for read mapping (GCF_000002655.1).


pep2geneID can be used on the command line like so:

```bash
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa
```

If you are using this for a different species/strain you can supply the appropriate dataset using the following options (in full transparency I have not extensively tested this):

```bash
# Aspergillus fumigatus Af293
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa --ensembl_host https://fungi.ensembl.org --ensembl_biomart fungi_mart --ensembl_dataset afumigatus_eg_gene
# Candida albicans
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa --ensembl_host https://fungi.ensembl.org --ensembl_biomart fungi_mart --ensembl_dataset calbicans_eg_gene
# Candida auris
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa --ensembl_host https://fungi.ensembl.org --ensembl_biomart fungi_mart --ensembl_dataset cauris_eg_gene
# Cryptococcus neoformans
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa --ensembl_host https://fungi.ensembl.org --ensembl_biomart fungi_mart --ensembl_dataset cneoformans_eg_gene
# Homo sapiens
Rscript /your/path/pep2geneID.R -f your-peptides.faa -o your-output.faa --ensembl_host https://www.ensembl.org --ensembl_biomart genes --ensembl_dataset hsapiens_gene_ensembl
```

Some peptide ID's may end in ".1". In the human example above, FASTA headers like "ENSP00000452345.1" need to be converted to "ENSP00000452345".
A simple way to do this is to cut the file:
```bash
cut -d'.' -f1 your-peptides.faa > your-peptides.trimmed.faa
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.


## Acknowledgements

This project was inspired by examples from the Bioconductor `biomaRt` vignette, available at:  
https://bioconductor.org/packages/release/bioc/vignettes/biomaRt/inst/doc/accessing_ensembl.html

For full details on which datasets to use, see the vignette above. A selection of human fungal pathogens have been shown in the examples above.


## License

[MIT](https://choosealicense.com/licenses/mit/)

