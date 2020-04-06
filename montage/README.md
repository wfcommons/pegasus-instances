<img src="https://workflowhub.org/assets/images/logo-horizontal.png" width="300" />
<img src="https://pegasus.isi.edu/wordpress/wp-content/uploads/2015/12/logo-dark.png" width=200 style="float: right" />

# Execution Traces for Montage Workflow

## Workflow Description

[Montage](http://montage.ipac.caltech.edu) is a toolkit for assembling Flexible
Image Transport System (FITS) images into custom mosaics. The test case
implemented as a
[Pegasus workflow](https://github.com/pegasus-isi/montage-workflow-v2) aim to
re-project, background correct and add astronomical images into custom mosaics.
This test case is composed of eight different tasks:

  1. `mProject` - reprojects a single image to the scale defined in an
     alternate FITS header template.
  2. `mDiffFit` - Run mDiff immediatly followed by mFitplane and check the
     first to decide whether to run the second.
  3. `mConcatFit` - Merge multiple plane fit parameter files (from mFitplane)
     into one file.
  4. `mBgModel` - A modelling/fitting program.
  5. `mBackground` - Subtracts a planar background from a FITS image.
  6. `mImgtbl` -  Extracts the FITS header geometry information from a set of
     files and creates an ASCII image metadata table which is used by several
     of the other programs.
  7. `mAdd` - Coadd the reprojected images in an input list to form an output
     mosaic with FITS header keywords specified in a header file.
  8. `mViewer` - Command line application or visualizing FITS images, overlaying
     content (grids, symbols, etc.) on them and creating PNG or JPEG files.

The figure below shows an overview of the Montage workflow structure:

<img src="docs/images/montage.png?raw=true" width="600">

### Research Publication

Details of the Montage workflow description, computational jobs, and
performance metrics can be found in the following research publication:

- M. Rynge, G. Juve, J. Kinney, J. Good, B. G. Berriman, A. Merrihew, and
  E. Deelman, "Producing an Infrared Multiwavelength Galactic Plane Atlas
  using Montage, Pegasus and Amazon Web Services," in 23rd Annual Astronomical
  Data Analysis Software and Systems (ADASS) Conference, 2013.

## Execution Traces

Execution traces are formatted according to the
[WorkflowHub JSON format](https://github.com/workflowhub/workflow-schema) for
describing workflow executions. Execution traces from different computing
platforms are organized into sub-folders.

Trace files are named using the following convention:
`montage-<COMPUTE_PLATFORM>-<SURVEY>-<DEGREE>-<RUN_ID>.json`, where:

- `<COMPUTE_PLATFORM>`: The compute platform where the actual Pegasus workflow
  was executed (e.g., `chameleon`).
- `<SURVEY>`: The data set and band to use for the mosaic (**2mass**:
  Two-Micron All-Sky Survey; **dss**: STScI Digitized Sky Survey).
- `<DEGREE>`: The size (in degrees) to be used for the width/height of the
  final mosaic.
- `<RUN_ID>`: The workflow execution identification.

### Workflow Structure

The Montage workflow structure depends on the _data set and band_
(`<SURVEY>`) used for the mosaic and the _size (in degrees)_ (`<DEGREE>`) to
be used for the width/height of the final mosaic. In this implementation,
the workflow has **3 bands** (red, blue, and green), where each band defines
"**a branch**" of the workflow. For each branch:

- The degree defines the number of tasks in a branch. The number of `mProject`
  and `mBackground` tasks are the same.
- An `mDiffFit` task is generated to from pairs of `mProjectPP` tasks. The
  number of `mDiffFit` tasks depends on the number of overlapped tiles.
- Each branch has only one instance of `mConcatFit`, `mBgModel`, `mImgtbl`,
  `mAdd`, and `mViewer` tasks, regardless the workflow degree.

An additional `mViewer` task at the bottom of the workflow combines all 3 bands
to create a colored JPEG.
