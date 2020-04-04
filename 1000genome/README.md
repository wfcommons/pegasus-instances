<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for 1000Genome Workflow

## Workflow Description

The 1000 genomes project provides a reference for human variation, having reconstructed the genomes of 2,504 individuals across 26 different populations. The test case implemented as a [Pegasus](https://pegasus.isi.edu) workflow identifies mutational overlaps using data from the 1000 genomes project in order to provide a null distribution for rigorous statistical evaluation of potential disease-related mutations. This test case is composed of five different tasks:

  1. `individuals` – This task fetches and parses the Phase 3 data from the 1000 genomes project per chromosome;
  2. `populations` – The populations task fetches and parses five super pop- ulations (African, Mixed American, East Asian, European, and South Asian), and a set of all individuals;
  3. `sifting` – This task computes the SIFT scores1 of all of the SNPs (single nu- cleotide polymorphisms) variants, as computed by the Variant Effect Predictor;
  4. `pair_overlap_mutations` – This task mea- sures the overlap in mutations (SNPs) among pairs of individu- als; and
  5. `frequency_overlap_mutations` – This task calculates the frequency of overlapping mutations across subsamples of certain individuals.

### Research Publication

Details of the 100Genome workflow description, computational jobs, and performance metrics can be found in the following research publication:

- Ferreira da Silva, R., Filgueira, R., Deelman, E., Pairo-Castineira, E., Overton, I. M., & Atkinson, M. (2019). Using Simple PID-inspired Controllers for Online Resilient Resource Management of Distributed Scientific Workflows. Future Generation Computer Systems, 95, 615–628. https://doi.org/10.1016/j.future.2019.01.015.
