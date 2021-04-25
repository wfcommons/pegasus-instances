<img src="https://wfcommons.org/images/wfcommons-horizontal.png" width="350" />
<img src="https://pegasus.isi.edu/documentation/_static/pegasus_circular_white_logo.png" width="100"/>

# Execution Instances for SRA Search Workflow

## Workflow Description

[SRA](https://www.ncbi.nlm.nih.gov/sra/) is a toolkit that provides a collection
of tools and libraries for using data in the INSDC Sequence Read Archives. Much
of the data submitted these days contain alignment information, for example in
BAM, Illumina export. txt, and Complete Genomics formats. The test case
implemented as a
[Pegasus workflow](https://github.com/pegasus-isi/sra-search-pegasus-workflow)
aim to download and align SRA data, using SRA Toolkit, Samtools and Bowtie2.
This test case is composed of four different tasks:

  1. `fasterq-dump` - Convert SRA data into fastq format.
  2. `bowtie2-build` - Index the genome with an FM Index (based on the
     Burrows-Wheeler Transform or BWT) to keep its memory footprint small.
  3. `bowtie2` - Aling sequencing reads to long reference sequences.
  4. `merge` - Merge a set of BAM files into a final tarball.

The figure below shows an overview of the SRA Search workflow structure:

<img src="docs/images/srasearch.png?raw=true" width="600">

## Execution Instances

Execution instances are formatted according to the
[WfCommons JSON format](https://github.com/wfcommons/workflow-schema) for
describing workflow executions. Execution instances from different computing
platforms are organized into sub-folders.

Instance files are named using the following convention:
`srasearch-<COMPUTE_PLATFORM>-<ACCESSION_LIST_SIZE>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<ACCESSION_LIST_SIZE>`: List of NCBI accession numbers.
- `<RUN_ID>`: The workflow execution identification.

### Workflow Structure

The SRA Search workflow structure depends exclusively on the number of NCBI
accession numbers (`<ACCESSION_LIST_SIZE>`), in which each accession number
is processed by a `fasterq-dump` task, each of each is followed by a `bowtie2`
task. The workflow has a single `bowtie2-build` task (regardless the number
of accessions). It also follows an upside down triangle of `merge` taks, i.e.
a `merge` task is added for each 25 `bowtie2` tasks, and if more than a single
`merge` task has been added, a final `merge` task (to merge all data from
previous merge tasks) is added.
