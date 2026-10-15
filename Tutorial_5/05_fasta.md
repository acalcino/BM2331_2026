# Populating your multi-fasta

Today is all about populating your multi-fasta. By this stage your fasta should have entries for every representative sequence from your particular gene family found in humans, but as the goal of our project is to describe the evolution of our gene family across the metazoa, we also need to sample sequences from representative species from other phylogenetic lineages.

![tree](images/tree.jpg)

This phylogenetic tree describes the relationship between the three major bilaterian clades `Lophotrochozoa, Ecdysozoa and Deuterotomia,` as well as the non-bilaterian clades `Cnidaria, Profera and Placozoa`. For whatever reason, in this tree `Ctenophora` is conspicuously missing.

Our goal today is to choose two representative species from each of the three bilaterian clades, as well as one non-bilaterian, and to isolate any members of your particular gene family that may exist in those species. To produce a robust phylogenetic tree of your gene family, more is always better. If you have time, I'd encourage you to sample as many species as possible but for now, aim for two from each clade for a total of eight species (2x Lophotrochozoa, 2x Ecdysozoa, 2x Deuterostomia, 1x non-bilaterian and your human orthologues).

## Methodology

There are many ways you could go about identifying the protein sequences you require and over the past few weeks, we've become familiar with a few excellent tools for completing this task.

### Text-based searches of NCBI

This is the easiest method to start obtatining results and the one students usually go for first becuase it seems easiest, however you will likely find that using this method is not comprehensive, will lead to lots of missing gene orthologues and will sometimes result in the inclusion of poorly annotated, non-homologous sequences.

### BLAST searches of genomes

Using BLAST is much more robust. Obtain the complete translated transcriptome sequence of your target species from [Ensembl](https://www.ensembl.org/), build a blastp database for it and then perform a BLAST search against this database using one of your human sequences as a query. To get the translated transcriptome file, click on `Genome Selector`, type in your species name and then on the results page, click the `FTP` link. Under `geneset`, right click on `pep.fa.bgz` and then `copy link address`. Go to the command line, navigate to the folder where you want to store the file and then use the `wget` command to download the file.

```bash
# An example command to download the Daphnia pulex transcriptome fasta
wget http://ftp.ebi.ac.uk/pub/ensemblorganisms/GCF/021/134/715/1/refseq/2022_07/geneset/pep.fa.bgz

```

### Use hmmsearch to identify sequences with a characteristic protein domain

In the previous tutorial we navigated to [Interpro](https://www.ebi.ac.uk/interpro/) and downloaded a Hidden Markov Model (hmm) for a domain which was characteristic of our particular gene family. We can use that same model to seach new non-human genomes too. Unlike with BLAST, you don't need to create a new database from an input transcriptome fasta file as you can use the transcriptome directly. If you've already downloaded the fasta as just explained in the BLAST section above, and you've still got the hmm from last week, then you're already ready to go. Construct your hmmsearch script, selecting appropriate significance cutoffs and output formats and then go for it.

## Workflow

