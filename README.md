# SomaLogic-Data

### File: example_data.adat

#### Overview

The `example_data.adat` is intended to provide existing and prospective
SomaLogic customers an example data file to enable analysis preparation prior
to receipt of SomaScan data, and also for those generally curious about the
SomaScan data deliverable. It is **not** intended to be used as a control
group for studies or provide any metrics for SomaScan data in general.

#### ADAT File Format

The ADAT file format is a SomaLogic-specific, tab-delimited text file designed
to store SomaScan study data. This format is intended to be flexible and
self-describing. The fields in this example file may be different than the
fields in the \*.adat file for your study. However, all \*.adat files are comprised
of four main sections arranged in the following order:

- `HEADER` - Study-level information about the SomaScan experiment and how the
data was processed.
- `COL_DATA` - Field names and type associated with the SOMAmer reagents
(columns).
- `ROW_DATA` - Field names and type associated with sample metadata (rows).
- `TABLE_BEGIN` - This section contains the experimental data organized into a
data matrix of SOMAmer Reagents (columns) by samples (rows). SomaScan measurements
are in relative flourescent units (RFU). The data block directly above the
measurement matrix describes the SOMAmer reagents and the data block to
to its left contains sample-specific (e.g. clinical) information.

#### Example File Description

This file, `example_data.adat`, contains a SomaScan V4 study from healthy 
normal individuals. The RFU measurements themselves and other identifiers 
have been altered to protect personally identifiable information (PII), 
but also retain underlying biological signal as much as possible. 
There are 192 total EDTA-plasma samples across two 96-well plate runs 
which are broken down by the following types:
* 170 clinical samples
* 10 calibrators (replicate controls for combining data across runs)
* 6 QC samples (replicate controls used to assess run quality)
* 6 Buffer samples (no protein controls)

#### Data Processing

The standard V4 data normalization procedure for EDTA-plasma samples was
applied to this dataset.

#### Parsers and programatic tools for \*.adat files

- R packge: [SomaDataIO](https://github.com/SomaLogic/SomaDataIO)
- Python module: [canopy.py](https://github.com/SomaLogic/Canopy)
