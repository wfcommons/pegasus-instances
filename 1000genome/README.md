<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for 1000Genome Workflow

## Workflow Description

The 1000 genomes project provides a reference for human variation, having
reconstructed the genomes of 2,504 individuals across 26 different populations.
The test case implemented as a
[Pegasus workflow](https://github.com/pegasus-isi/1000genome-workflow)
identifies mutational overlaps using data from the 1000 genomes project in
order to provide a null distribution for rigorous statistical evaluation of
potential disease-related mutations. This test case is composed of five
different tasks:

  1. `individuals` – This task fetches and parses the Phase 3 data from the
     1000 genomes project per chromosome;
  1. `individuals_merge` – This task combines all outputs of the `individuals`
     tasks into a single file;
  1. `sifting` – This task computes the SIFT scores1 of all of the SNPs (single
     nucleotide polymorphisms) variants, as computed by the Variant Effect
     Predictor;
  1. `mutation_overlap` – This task measures the overlap in mutations
     (SNPs) among pairs of individuals; and
  1. `frequency_overlap_mutations` – This task calculates the frequency of
     overlapping mutations across subsamples of certain individuals.

The figure below shows **a branch** of the 1000Genome workflow for the analysis
of a **single chromossome**.

<img src="docs/images/1000genome.png?raw=true" width="450">

### Research Publication

Details of the 100Genome workflow description, computational jobs, and
performance metrics can be found in the following research publication:

- Ferreira da Silva, R., Filgueira, R., Deelman, E., Pairo-Castineira, E.,
  Overton, I. M., & Atkinson, M. (2019). Using Simple PID-inspired Controllers
  for Online Resilient Resource Management of Distributed Scientific Workflows.
  Future Generation Computer Systems, 95, 615–628.
  https://doi.org/10.1016/j.future.2019.01.015.

## Execution Traces

Execution traces are formatted according to the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema) for
describing workflow executions. Execution traces from different computing
platforms are organized into sub-folders.

Trace files are named using the following convention:
`1000genome-<COMPUTE_PLATFORM>-<NUM_CH>ch-<NUM_SEQ>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<NUM_CH>`: The number of chromosomes evaluated in the workflow execution.
- `<NUM_SEQ>`: The number of sequences per chromosome file.
- `<RUN_ID>`: The workflow execution identification.

The number of chromosomes (`<NUM_CH>`) impact the number of tasks in the
workflow, while the number of sequences per chromosome file (`<NUM_SEQ>`)
impacts the workflow data footprint (both input and output data), as well as
task runtime.

### Workflow Structure

The 1000Genome workflow structure depends on the _number of chromosses_
(`<NUM_CH>`) evaluated and the _number of sequences per chromossome_
(`<NUM_SEQ>`). For a *single branch* (i.e., one chromossome):

- Each `individuals` task evaluates 1000 sequences, thus the number of
  `individuals` tasks for a single branch is defined as `<NUM_SEQ>/1000`;
- There is only _one_ `individuals_merge` task per branch;
- There is only _one_ `sifting` task per branch;
- The number of `mutation_overlap` and `sifting` tasks per branch is driven
  by the number of **populations** (e.g., African, Mixed American, East Asian,
  European, South Asian) being evaluated.
