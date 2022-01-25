![Build](https://github.com/wfcommons/pegasus-instances/workflows/Build/badge.svg)
[![DOI](https://zenodo.org/badge/74868669.svg)](https://zenodo.org/badge/latestdoi/74868669)

<a href="https://wfcommons.org" target="_blank"><img src="https://wfcommons.org/images/wfcommons-horizontal.png" width="350"/></a>

<img src="https://pegasus.isi.edu/documentation/_static/pegasus_circular_white_logo.png" width="100"/>

# Pegasus Workflow Execution Instances

This repository contains workflow execution instances generated from
[Pegasus](http://pegasus.isi.edu) workflow executions. The instances
hosted in this repository use the
[WfCommons JSON format](https://github.com/wfcommons/workflow-schema)
for describing workflow executions.

#### Repository Structure

Workflow execution instances are organized into sub-folders within this
repository. Each sub-folder represents a _workflow application_, which
itself contains sub-folders for workflow executions in different
_computing platforms_.

#### Workflow Simulator

The execution instances provided in this repository are compatible to any
[simulator framework](https://wfcommons.org/simulation) that implements
the [WfCommons JSON format](https://github.com/wfcommons/workflow-schema).

## Summary of Workflow Execution Instances

| Application | Science Domain | Category | Computing Platforms | # Execution Instances |
| --- | --- | --- | --- | --- |
| 1000Genome | Bioinformatics | Data-intensive | 1 | 22 |
| Cycles | Agroecosystem | Compute-intensive | 1 | 24 |
| Epigenomics | Bioinformatics | Data-intensive | 1 | 26 |
| Montage | Astronomy | Compute-intensive | 1 | 17 |
| Seismic Cross Correlation | Seismology | Data-intensive | 1 | 11 |
| SoyKB | Bioinformatics | Data-intensive | 1 | 10 |
| SRA Search | Bioinformatics | Data-intensive | 1 | 25 |
