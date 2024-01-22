
# SomaLogic-Data <a href="https://github.com/SomaLogic/SomaLogic-Data"><img src="figures/logo.png" align="right" height="120" alt="SomaLogic-Data GitHub" /></a>


The ADAT files included in this repository are intended to provide
existing and prospective SomaLogic customers an example data file
to enable analysis preparation prior to receipt of SomaScan data,
and also for those generally curious about the SomaScan data deliverable.
Data in this file is **not** intended for biological analysis
purposes or to provide any metrics for SomaScan data in general.

---------------------


## Files 

* `example_data.adat`
* `example_data_v4.1_plasma.adat`


## Installation

The example ADAT files in this repository can be retrieved in one of two ways:

1. Cloning the repository to your local machine

1. Using `wget` to retrieve individual ADAT files from the repository;
   see examples below

```bash
# Retrieve just the 5k (v4.0) ADAT
wget https://github.com/SomaLogic/SomaLogic-Data/raw/master/example_data.adat

# Retrieve just the 7k (v4.1) ADAT
wget https://github.com/SomaLogic/SomaLogic-Data/raw/master/example_data_v4.1_plasma.adat
```


## SomaScan Versions

| commercial name | menu version | size  | example file                     |
| --------------- | ------------ | ----- | -------------------------------- |
| 5k              | V4           | 5284  | `example_data.adat`              |
| 7k              | v4.1         | 7596  | `example_data_v4.1_plasma.adat`  |
| 11k             | v5.0         | 11083 | `NA`                             |


## ADAT File Format

The ADAT file format is a SomaLogic-specific, tab-delimited text file designed
to store SomaScan study data. This format is intended to be flexible and
self-describing. The fields in this example file may be different than the
fields in the \*.adat file for your study. However, all \*.adat files are
comprised of four main sections arranged in the following order:

- `HEADER` - Study-level information about the SomaScan experiment and how the
data was processed.
- `COL_DATA` - Field names and type associated with the SOMAmer reagents
(columns).
- `ROW_DATA` - Field names and type associated with sample information (rows).
- `TABLE_BEGIN` - This section contains the experimental data organized into a
data matrix of SOMAmer Reagents (columns) by samples (rows). SomaScan
measurements are in relative flourescent units (RFU). The data block directly
above the measurement matrix describes the SOMAmer reagents and the data block
to its left contains sample-specific (e.g. clinical) information.


## Example File Description

The file, `example_data.adat`, contains a SomaScan V4.0 study from a set of
human samples. The RFU measurements themselves and other identifiers
have been altered to protect personally identifiable information (PII),
but also retain underlying biological signal as much as possible.
There are 192 total EDTA-plasma samples from four plate runs
which are broken down by the following types:
* 170 clinical samples
* 10 calibrators (replicate controls for combining data across runs)
* 6 QC samples (replicate controls used to assess run quality)
* 6 Buffer samples (no protein controls)

The second file, `example_data_v4.1_plasma.adat`, contains a SomaScan v4.1
study from the same set of human samples.
RFU measurements have been altered protect PII in this file as well.
There are 163 EDTA Plasma samples from four 96-well plate runs which
include the following:
* 163 clinical samples
* 20 calibrators
* 12 QC samples 
* 12 Buffer samples 


## Data Processing

The standard V4 data normalization procedure for EDTA-plasma samples was
applied to this dataset.


## Sample and Analyte Annotations

In a standard SomaLogic ADAT, the section of information that
sits directly above the measurement data (RFU data matrix) is
the column meta data, which contains detailed information
and annotations about the analytes, `SeqIds`, and their targets.
See section below for further information about available
fields and their descriptions.

### Analyte Annotations:
Information describing the *analytes* is found to the above
the data matrix in a standard SomaLogic ADAT. This information may
consist of the any or all of the following:

| __Field__          | __Description__                       | __Example__    |
| :----------------- | :------------------------------------ | :------------- |
| SeqId                         | SomaLogic sequence identifier                                    | 2182-54\_1      |
| SeqidVersion                  | Version of SOMAmer sequence                                      | 2              |
| SomaId                        | Target identifier, of the form SLnnnnnn (8 characters in length) | SL000318       |
| TargetFullName                | Target name curated for consistency with UniProt name            | Complement C4b |
| Target                        | SomaLogic Target Name                                            | C4b            |
| UniProt                       | UniProt identifier(s)                                            | P0C0L4  P0C0L5 |
| EntrezGeneID                  | Entrez Gene Identifier(s)                                        | 720 721        |
| EntrezGeneSymbol              | Entrez Gene Symbol names                                         | C4A C4B        |
| Organism                      | Protein Source Organism                                          | Human          |
| Units                         | Relative Fluorescence Units                                      | RFU            |
| Type                          | SOMAmer target type                                              | Protein        |
| Dilution                      | Dilution mix assignment                                          | 0.01%          |
| PlateScale\_Reference         | PlateScale reference value                                       | 1378.85        |
| CalReference                  | Calibration sample reference value                               | 1378.85        |
| medNormRef\_ReferenceRFU      | Median normalization reference value                             | 490.342        |
| Cal\_V4\_\<YY\>\_\<SSS\>\_\<PPP\> | Calibration scale factor (for given Year\_Study\_Plate)      | 0.64           |
| ColCheck                      | QC acceptance criteria across all plates/sets                    | PASS           |
| QcReference\_\<LLLLL\>        | QC sample reference value (for given QC lot)                     | PASS           |
| CalQcRatio\_V4\_\<YY\>\_\<SSS\>\_\<PPP\> | Post calibration median QC ratio to reference (for given Year\_Study\_Plate) | 1.04 |

### Sample Annotations:
Information describing the *samples* is typically found to the left of
the data matrix in a standard SomaLogic ADAT. This information may
consist of clinical information provided by the client, or run-specific
diagnostic information included for assay quality control. Below are
some examples of what may be present in this section:

| __Field__         | __Description__                                   | __Examples__   |
| :---------------- | :------------------------------------------------ | :------------- |
| PlateId           | Plate identifier                                  | V4-18-004\_001, V4-18-004\_002 |
| ScannerID         | Scanner used to analyze slide                     | SG12064173, SG14374437 |
| PlatePosition     | Location on 96 well plate (A1-H12)                | A1, H12              |
| SlideId           | Agilent slide barcode                             | 258495800001         |
| Subarray          | Agilent subarray (1 – 8)                          | 1,8                  |
| SampleId          | 1st form is Subject Identifier, 2nd form (calibrators, buffers) | 2031   |
| SampleType        | 1st form for clinical samples (Sample), 2nd form as above       | Sample, QC, Calibrator, Buffer |
| PercentDilution   | Highest concentration the SOMAmer dilution groups | 20                   |
| SampleMatrix      | Sample matrix                                     | Plasma-PPT           |
| Barcode           | 1D Barcode of aliquot                             | S622225              |
| Barcode2d         | 2D Barcode of aliquot                             | 9876543210           |
| SampleNotes       | Assay team sample observation                     | Cloudy, Low sample volume, Reddish |
| SampleDescription | Supplemental sample information                   | Plasma QC 1          |
| AssayNotes        | Assay team run observation                        | Beads aspirated, Leak/Hole, Smear  |
| TimePoint         | Sample time point                                 | Baseline             |
| ExtIdentifier     | Primary key for Subarray                          | EXID40000000032037   |
| SsfExtId          | Primary key for sample                            | EID102733            |
| SampleGroup       | Sample group                                      | A, B                 |
| SiteId            | Collection site                                   | SomaLogic            |
| TubeUniqueID      | Unique tube identifier                            | 2031                 |
| CLI               | Cohort definition identifier                      | CLI6006F001          |
| HybControlNormScale | Hybridization control scale factor              | 0.948304             |
| RowCheck          | Normalization acceptance criteria for all row scale factors | PASS, FLAG |
| NormScale\_0\_5   | Median signal normalization scale factor (0.5% mix)    | 1.02718         |
| NormScale\_0\_005 | Median signal normalization scale factor (0.005% mix)  | 1.119754        |
| NormScale\_20     | Median signal normalization scale factor (20% mix)     | 0.996148        |

---------------------


## Parsers and Programatic Tools for ADAT Files

- R package: [SomaDataIO](https://github.com/SomaLogic/SomaDataIO)
- Python module: [Canopy](https://github.com/SomaLogic/Canopy)
- Digital Tools: [DataDelve Statistics](https://somalogic.com/datadelve-statistics/)


---------------

[SomaLogic-Data](https://github.com/SomaLogic/SomaLogic-Data/) 
was developed by the Bioinformatics Dept. at 
[SomaLogic Operating Co., Inc.](http://www.somalogic.com)
