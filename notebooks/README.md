# AI-Assisted Network Performance Management Decision Support

This project is a proof of concept for AI-assisted Network Performance Management (NPM) decision support using a realistic synthetic Telkom cell degradation scenario.

The POC shows how noisy multi-source network data can be converted into a clear engineer-facing incident output:

1. Detect abnormal or deteriorating cell behaviour.
2. Cluster related alarms, KPIs, counters, complaints, drive tests, and topology/config changes.
3. Infer a likely root cause with explainable evidence.
4. Present the output as Facts, AI Inference, and Recommendation.
5. Estimate investigation-time and alarm-noise reduction benefits.

## Project Structure

```text
data/
  raw/                         Synthetic source datasets
  processed/                   Generated model outputs
src/npm_poc/
  data_loader.py               CSV loading and timestamp parsing
  feature_engineering.py       Unified cell time-window feature table
  detection.py                 Degradation and anomaly detection
  clustering.py                Incident event clustering
  root_cause.py                Explainable RCA scoring
  reporting.py                 Facts / inference / recommendation report
run_pipeline.py                End-to-end POC runner
generate_telkom_cell_degradation_data.py
```

## Run The POC

From the project root:

```powershell
python .\generate_telkom_cell_degradation_data.py
python .\run_pipeline.py
```

## Run In Google Colab

Open this notebook in Colab:

```text
notebooks/telkom_npm_poc_colab.ipynb
```

Recommended Colab flow:

1. Upload the project folder or a ZIP containing the `data/` folder.
2. Open `notebooks/telkom_npm_poc_colab.ipynb`.
3. Run the cells from top to bottom.
4. If Colab cannot find `data/raw`, run the notebook's upload helper cell and upload the ZIP.

The notebook is self-contained for the modelling workflow. It does not need to import the local `src/` package.

Generated outputs:

```text
data/processed/cell_window_features.csv
data/processed/detected_degradations.csv
data/processed/incident_clusters.json
data/processed/rca_report.json
data/processed/engineer_report.md
```

## Current Scenario

The injected incident is:

```text
Incident ID: INC-20260915-JHB-CBD-003-B
Operator: Telkom
Cell: JHB-CBD-003-B
Scenario: LTE cell degradation
Likely root cause: Transport backhaul congestion after microwave protection-path misconfiguration
```

The system should identify the degraded cell, group related evidence, and produce a recommendation to check or roll back the transport configuration change.

