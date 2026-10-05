# backend-machineL

Data, trained model files, and the modelling notebook for the SATNAC Topic 5 proof of concept: AI-assisted Network Performance Management on a synthetic Telkom cell-degradation incident.

The incident is `JHB-CBD-003-B` on 15 Sep 2026. The leading cause in the checked-in outputs is transport backhaul congestion. This repo has no web server. The engineer desk is the sibling repo `frontend-satnac`.

## What you need

- Python 3.10 or newer
- For a local notebook run: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, and Jupyter
- For Google Colab: a Colab account. Colab already includes those libraries

## What is already in the repo

You do not need to generate data before opening the notebook or the desk. These files are checked in:

| Path | What it is |
| --- | --- |
| `data/raw/` | Source CSVs: KPIs, counters, alarms, drive tests, complaints, topology |
| `data/processed/` | Pipeline outputs the desk reads, including `engineer_report.md`, `rca_report.json`, and `incident_clusters.json` |
| `data/dataset_manifest.json` | Seed, date range, and row counts |
| `model/` | Saved classifier files (`isolation_forest_model.pkl`, `logistic_regression_model.pkl`, `random_forest_model.pkl`) |
| `notebooks/telkom_npm_poc_colab.ipynb` | End-to-end notebook: load, detect, cluster, score causes, write a report |

`data/README.md` describes each CSV.

## Run the notebook locally

From this folder, create a virtual environment and install the notebook libraries:

```powershell
py -3 -m venv .venv
.\.venv\Scripts\Activate.ps1
py -3 -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

On macOS or Linux, use `python3` instead of `py -3`, and activate with `source .venv/bin/activate`.

Start Jupyter with this repo as the working directory, then open the notebook and run the cells from top to bottom:

```powershell
jupyter notebook notebooks/telkom_npm_poc_colab.ipynb
```

The first code cell looks for `data/raw/telkom_network_kpis.csv` from the kernel’s current directory. It should print `Raw data folder exists: True`. If it prints `False`, the kernel started inside `notebooks/`. Run this once, then re-run the setup cell:

```python
import os
os.chdir("..")
```

The notebook writes new files with a `_colab` suffix under `data/processed/`. It leaves the existing processed files in place. The desk keeps using those existing files until someone replaces them and rebuilds the frontend snapshot.

## Run the notebook in Google Colab

1. Upload this repo, or a zip that contains the `data/` folder, into Colab.
2. Open `notebooks/telkom_npm_poc_colab.ipynb`.
3. Run the cells from top to bottom.
4. If the setup cell prints `Raw data folder exists: False`, uncomment and run the upload-helper cell, upload the zip, then re-run the setup cell.

## How this connects to the desk

`frontend-satnac` must sit next to this repo:

```text
SATNAC-HACK/
  backend-machineL/
  frontend-satnac/
```

From `frontend-satnac`, `npm run snapshot` reads `data/raw` and `data/processed` here and rewrites the desk snapshot. See that repo’s README for how to start the desk.
