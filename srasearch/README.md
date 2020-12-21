<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for SRA Search Workflow

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
  4. `merge` - .

The figure below shows an overview of the SRA Search workflow structure:

<img src="docs/images/srasearch.png?raw=true" width="600">

## Execution Traces

Execution traces are formatted according to the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema) for
describing workflow executions. Execution traces from different computing
platforms are organized into sub-folders.

Trace files are named using the following convention:
`srasearch-<COMPUTE_PLATFORM>-<ACCESSION_LIST_SIZE>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<ACCESSION_LIST_SIZE>`: List of NCBI accession numbers.
- `<RUN_ID>`: The workflow execution identification.

### Workflow Structure
