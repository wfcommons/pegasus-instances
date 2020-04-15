[![Build Status][travis-badge]][travis-link]

<a href="https://workflowhub.org" target="_blank"><img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" /></a>

<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Pegasus Workflow Execution Traces

This repository contains workflow execution traces generated from
[Pegasus](http://pegasus.isi.edu) workflow executions. The traces
hosted in this repository use the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema)
for describing workflow executions.

#### Repository Structure

Workflow execution traces are organized into sub-folders within this
repository. Each sub-folder represents a _workflow application_, which
itself contains sub-folders for workflow executions in different
_computing platforms_.

#### Workflow Simulator

The execution traces provided in this repository are compatible to any
[simulator framework](https://workflowhub.org/simulator.html) that implements
the [WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema).
Specifically, the workflow execution traces hosted here were generated using
the `wrench-pegasus-parser.py` tool that is distributed as part of the
[WRENCH-Pegasus](https://github.com/wrench-project/pegasus) simulator.


## Summary of Workflow Execution Traces

| Application | Science Domain | Computing Platforms | # Execution Traces |
| --- | --- | --- | --- |
| 1000Genome | Bioinformatics | 1 | 22 |
| Cycles | Agroecosystem | 1 | 24 |
| Epigenomics | Bioinformatics | 1 | 26 |
| Montage | Astronomy | 1 | 8 |
| Seismic Cross Correlation | Seismology | 1 | 11 |
| SoyKB | Bioinformatics | 1 | 10 |


[travis-badge]:             https://travis-ci.org/workflowhub/pegasus-traces.svg?branch=master
[travis-link]:              https://travis-ci.org/workflowhub/pegasus-traces
