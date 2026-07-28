# 4G LTE Throughput Prediction and Signal Quality Analysis

A telecom-focused machine learning project for exploring how LTE radio,
mobility, and contextual measurements relate to downlink throughput.

## Project Status

> **Status:** Ongoing — initial data validation complete

This repository is being developed as a focused machine learning comeback
project. The first version is intentionally limited to one main notebook
covering data audit, exploratory analysis, regression baselines, model
evaluation, and telecom-oriented interpretation.

No final model result is claimed yet.

The 135 traces have been combined and structurally cleaned in the main
notebook. Numeric placeholders are represented as missing values, exact
duplicate rows have been removed, and timestamps have been parsed. Confirmed
invalid serving- and neighbour-signal measurements are represented as missing
values without removing their rows. Download state and unusual static-speed
readings have also been examined and documented before exploratory analysis.

## Start Here

- Read the
  [LTE domain notes](./notebooks/README.md) for the story behind the dataset,
  the meaning of its radio metrics, and the questions that still need auditing.
- Open the
  [main analysis notebook](./notebooks/01_lte_throughput_analysis.ipynb) to
  follow the project from data discovery onward.

The notebook is intentionally developed one understandable step at a time.

## Problem Statement

Mobile users can experience different throughput even when the received signal
appears relatively strong. Downlink performance can also be influenced by
signal quality, interference, channel conditions, mobility, serving-cell
distance, network mode, and other contextual factors.

This project investigates:

> How well can LTE radio and mobility metrics predict downlink throughput?

The initial machine learning task is supervised regression with `DL_bitrate`
as the target candidate.

## Objectives

- inspect the structure and quality of a real-world LTE measurement dataset;
- explore relationships between radio metrics and downlink throughput;
- establish a simple non-ML baseline;
- compare a small number of regression models;
- evaluate performance with MAE, RMSE, and R²;
- compare random splitting with trace- or group-aware validation;
- inspect large prediction errors;
- explain findings using machine learning and telecommunication reasoning.

## Dataset

This project uses the
[4G LTE Speed Dataset and Bandwidth](https://www.kaggle.com/datasets/aeryss/lte-dataset)
published on Kaggle.

The dataset is associated with:

> D. Raca, J. J. Quinlan, A. H. Zahran, and C. J. Sreenan,
> “Beyond Throughput: A 4G LTE Dataset with Channel and Context Metrics,”
> ACM Multimedia Systems Conference, 2018.

Research archive:

- <https://cora.ucc.ie/handle/10468/6400>

Downloaded files are excluded from Git.

To download the dataset locally:

```powershell
$downloadCode = @'
import kagglehub

path = kagglehub.dataset_download(
    "aeryss/lte-dataset",
    output_dir="./data",
)
print("Dataset downloaded to:", path)
'@

uv run python -c $downloadCode
```

## Candidate Variables

The final feature set will only be selected after the data audit.

Candidate variables may include:

- RSRP;
- RSRQ;
- RSSI;
- SNR;
- CQI;
- velocity;
- serving-cell distance;
- network mode;
- operator;
- cell identifier;
- download state;
- neighbouring-cell metrics;
- context measurements.

Not all columns will necessarily be used. Missing values, sentinel values,
leakage, trace identity, temporal dependence, and technical meaning must be
examined first.

## Planned Workflow

1. Define the telecom and machine learning problem.
2. Inspect downloaded files and identify trace structure.
3. Audit schema, types, missing values, duplicates, and suspicious values.
4. Explore the target and relevant radio/context variables.
5. Decide how idle and active download records should be treated.
6. Build a mean prediction baseline.
7. Train an interpretable linear model.
8. Compare selected nonlinear regression models.
9. Evaluate with MAE, RMSE, and R².
10. Compare random validation with trace/group-aware validation.
11. Analyze residuals and large prediction errors.
12. Interpret findings in a telecom context.
13. Document limitations.

## Repository Structure

```text
17_4G_LTE_Throughput_Prediction/
├── data/                  # Local dataset, excluded from Git
├── images/                # Selected figures for documentation
├── notebooks/
│   ├── 01_lte_throughput_analysis.ipynb
│   └── README.md           # Telecom domain notes
├── .gitignore
├── .python-version
├── README.md
├── pyproject.toml
└── uv.lock
```

The local folder uses a numbered Title Case convention, while the GitHub
repository uses the URL-friendly name `4g-lte-throughput-prediction`.

## Environment

- Windows 11
- PowerShell 7
- Python 3.12.13
- uv
- VS Code / Jupyter
- NumPy
- pandas
- Matplotlib
- Seaborn
- scikit-learn
- kagglehub

## Local Setup

Clone the repository:

```powershell
git clone https://github.com/Zendin110206/4g-lte-throughput-prediction.git
Set-Location .\4g-lte-throughput-prediction
```

Install the locked environment:

```powershell
uv sync
```

Download the dataset using the command in [Dataset](#dataset).

Open the project:

```powershell
code .
```

Run JupyterLab if needed:

```powershell
uv run jupyter lab
```

## Evaluation Plan

The initial metrics are:

- **MAE** — average absolute prediction error;
- **RMSE** — gives more penalty to large errors;
- **R²** — proportion of variance explained relative to a mean baseline.

Measurements inside the same trace may be temporally related. A random row
split can therefore produce optimistic performance. The project plans to
compare random splitting with trace- or group-aware validation after a usable
trace identifier is established.

## Scope and Limitations

This is a learning and portfolio project based on a public dataset.

It is not:

- a live operator monitoring system;
- a production throughput estimator;
- a radio network planning tool;
- an official operator performance benchmark;
- evidence that radio metrics alone fully explain user throughput.

Throughput may also depend on unavailable factors such as scheduler state,
allocated bandwidth, traffic load, backhaul, device capability, protocol
behavior, and application characteristics.

## Author

**Muhammad Zaenal Abidin Abdurrahman**  
Telecommunication Engineering Undergraduate, Telkom University

- GitHub: [Zendin110206](https://github.com/Zendin110206)
- LinkedIn: [zendin1102](https://www.linkedin.com/in/zendin1102/)
