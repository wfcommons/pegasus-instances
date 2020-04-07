<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for Soybean Workflow (SoyKB)

## Workflow Description

The Soybean workflow (SoyKB) is a genomics pipeline that re-sequences soybean
germplasm lines selected for desirable traits such as oil, protein, soybean
cyst nematode resistance, stress resistance, and root system architecture.
The workflow implemented as a
[Pegasus workflow](https://github.com/pegasus-isi/Soybean-Workflow) provides
a Single Nucleotide Polymorphism (SNP) and injection/deletion (indel)
identification and analysis pipeline using the
[GATK](https://www.broadinstitute.org/gatk) haplotype caller and a soybean
reference genome. The workflow is composed of fourteen different tasks:

  1. `alignment_to_reference`
  2. `sort_sam`
  3. `dedup`
  4. `add_replace`
  5. `realign_target_creator`
  6. `indel_realign`
  7. `haplotype_caller`
  8. `genotype_gvcfs`
  9. `combine_variants`
  10. `merge_gvcfs`
  11. `select_variants_indel`
  12. `select_variants_snp`
  13. `filtering_indel`
  14. `filtering_snp`

The figure below shows an overview of the SoyKB workflow structure:

<img src="docs/images/soykb.png?raw=true" width="650">

### Research Publication

Details of the SoyKB workflow description, computational jobs, and
performance metrics can be found in the following research publication:

- Y. Liu, S. M. Khan, J. Wang, M. Rynge, Y. Zhang, S. Zeng, S. Chen, J. V.
  Maldonado dos Santos, B. Valliyodan, P. P. Calyam, N. Merchant, H. T.
  Nguyen, D. Xu, and T. Joshi, “PGen: large-scale genomic variations analysis
  workflow and browser in SoyKB,” BMC Bioinformatics, vol. 17, iss. 13, p.
  337, 2016. https://doi.org/10.1186/s12859-016-1227-y

## Execution Traces

Execution traces are formatted according to the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema)
for describing workflow executions. Execution traces from different
computing platforms are organized into sub-folders.

Trace files are named using the following convention:
`soykb-<COMPUTE_PLATFORM>-<NUM_FASTQ>-<NUM_CH>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<NUM_FASTQ>`:
- `<NUM_CH>`:
- `<RUN_ID>`: The workflow execution identification.

### Workflow Structure

The SoyKB workflow structure depends on the _number of FASTQ files_
(`<NUM_FASTQ>`) and the _number of chromossomes_ (`<NUM_CH>`). In this
implementation, the workflow has a subset of tasks that form **pipelines**,
which are defined as follows:

- The number of pipelines is defined as half of the number of FASTQ files
  (i.e., `<NUM_FASTQ>/2`), since each `alignment_to_reference` task processes
  two FASTQ files.
- Each pipeline has only one instance of `alignment_to_reference`, `sort_sam`,
  `dedup`, `add_replace`, `realign_target_creator`, and `indel_realign` tasks.
- The number of `haplotype_caller` tasks is proportional to the number of
  chromossomes (`<NUM_CH>`).

For the **entire workflow**:

- The number of `genotype_gvcfs` tasks is proportional to the number of
  chromossomes (`<NUM_CH>`). The number of `haplotype_caller` parent tasks
  for each `genotype_gvcfs` is equal to the number of pipelines, however
  each task analyzes data from a single chromossome.
- There is only one instance for each of the following tasks:
  `combine_variants`, `merge_gvcfs`, `select_variants_indel`,
  `select_variants_snp`, `filtering_indel`, and `filtering_snp`.
