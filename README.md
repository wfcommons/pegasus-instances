![Build](https://github.com/wfcommons/pegasus-traces/workflows/Build/badge.svg)

<a href="https://wfcommons.org" target="_blank"><img src="https://wfcommons.org/images/wfcommons-horizontal.png" width="350" /></a>

<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Pegasus Workflow Execution Traces

This repository contains workflow execution traces generated from
[Pegasus](http://pegasus.isi.edu) workflow executions. The traces
hosted in this repository use the
[WfCommons JSON format](https://github.com/wfcommons/workflow-schema)
for describing workflow executions.

#### Repository Structure

Workflow execution traces are organized into sub-folders within this
repository. Each sub-folder represents a _workflow application_, which
itself contains sub-folders for workflow executions in different
_computing platforms_.

#### Workflow Simulator

The execution traces provided in this repository are compatible to any
[simulator framework](https://wfcommons.org/simulators) that implements
the [WfCommons JSON format](https://github.com/wfcommons/workflow-schema).

## Summary of Workflow Execution Traces

| Application | Science Domain | Category | Computing Platforms | # Execution Traces |
| --- | --- | --- | --- | --- |
| 1000Genome | Bioinformatics | Data-intensive | 1 | 22 |
| Cycles | Agroecosystem | Compute-intensive | 1 | 24 |
| Epigenomics | Bioinformatics | Data-intensive | 1 | 26 |
| Montage | Astronomy | Compute-intensive | 1 | 13 |
| Seismic Cross Correlation | Data-intensive | Seismology | 1 | 11 |
| SoyKB | Bioinformatics | Data-intensive | 1 | 10 |
| SRA Search | Bioinformatics | Data-intensive | 1 | 25 |
