<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for Cycles Workflow

## Workflow Description

Cycles is a user-friendly, multi-crop, multi-year, process-based Agroecosystem
model with daily time step simulations of crop production and the water, carbon
(C) and nitrogen (N) cycles in the soil-plant-atmosphere continuum. The model
can simulate perturbations of biogeochemical processes caused by agronomic
practices such as tillage, irrigation, organic and inorganic nutrient
applications, annual and perennial crops selection, grain and forage harvest,
poly-cultures, relay cropping and grazing. Cycles allows unlimited crop species
to be specified by the user. The workflow is composed of seven different tasks:

  1. `baseline_cycles`: computes the model reference or baseline.
  2. `fertilizer_increase_cycles`: Cycles execution with increased fertilizer
     rate of 10% – key to forecasting the economic impact of grain yields.
  3. `cycles`: Cycles execution.
  4. `cycles_output_summary`: aggregates and summarizes all outputs for a
     single crop.
  5. `cycles_fertilizer_increase_output_parser`
  6. `cycles_fertilizer_increase_output_summary`: aggregates and summarizes all
     outputs for a single crop.
  7. `cycles_plots`: ensembles all summaries and produce visualization outputs.

The figure below shows an overview of the Cycles workflow structure:

<img src="docs/images/cycles.png?raw=true" width="750">

### Research Publication

Details of the Cycles workflow description, computational jobs, and
performance metrics can be found in the following research publication:

- Ferreira da Silva, R., Mayani, R., Shi, Y., Kemanian, A. R., Rynge, M., &
  Deelman, E. (2019). "Empowering Agroecosystem Modeling with HTC Scientific
  Workflows: The Cycles Model Use Case". In First International Workshop on
  Big Data Tools, Methods, and Use Cases for Innovative Scientific Discovery
  (BTSD) (pp. 4545–4552). https://doi.org/10.1109/BigData47090.2019.9006107

## Execution Traces

Execution traces are formatted according to the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema)
for describing workflow executions. Execution traces from different
computing platforms are organized into sub-folders.

Trace files are named using the following convention:
`cycles-<COMPUTE_PLATFORM>-<LOCATIONS>-<CROPS>-<PARAMS>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<LOCATIONS>`: The number of points of the spatial grid cell.
- `<CROPS>`: Number of crops being evaluated.
- `<PARAMS>`: Number of parameter values from the simulation matrix.
- `<RUN_ID>`: The workflow execution identification.

### Workflow Structure

The Cycles workflow structure depends on the _number of points_ (`<LOCATIONS>`),
_number of crops_ (`<CROPS>`), and the _number of parameter values_
(`<PARAMS>`). In this implementation, the workflow is composed of **branches**
that represent each point of the spatial grid. For each branch:

- The number of tasks is first steered by the number of different crops being
  evaluated.
- For each **tuple** of `(point, crop)`, a number of product combinations
  defined by the number of parameters will generate workflow segments for
  `baseline_cycles`, `fertilizer_increase_cycles`, `cycles`, and
  `cycles_fertilizer_increase_output_parser` tasks.
- For each **tuple** of `(point, crop)`, there is a `cycles_output_summary`,
  and a `cycles_fertilizer_increase_output_summary` tasks per crop type.
- There is a `cycles_plots` task for each crop type in the workflow - e.g.,
  if the workflow evaluates two crops, then there will be 2 tasks of each type.
