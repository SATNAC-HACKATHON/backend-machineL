# Synthetic Telkom Cell Degradation Dataset

This folder contains a deterministic synthetic dataset for the project scenario described in the source document: AI-assisted Network Performance Management decision support for a cell degradation incident.

The injected scenario is a Telkom LTE cell degradation at `JHB-CBD-003-B` on `2026-09-15` from `08:45` to `13:45`. The modeled root cause is transport backhaul congestion after a microwave protection-path configuration change.

## Files

| File | Purpose |
| --- | --- |
| `dataset_manifest.json` | Dataset metadata, seed, date range, row counts, and source note. |
| `raw/telkom_network_kpis.csv` | 15-minute network KPI time series with accessibility, retainability, throughput, latency, RF quality, PRB utilization, anomaly score, and labels. |
| `raw/telkom_performance_counters.csv` | RRC/E-RAB attempts and failures, drops, PRB counters, packet loss, and transport discard packets. |
| `raw/telkom_alarms.csv` | Correlated incident alarms plus unrelated background/noise alarms. |
| `raw/telkom_drive_test_logs.csv` | RF and throughput samples for serving cells, including failed tests during the degradation. |
| `raw/telkom_customer_complaints.csv` | Customer trouble tickets with classification, priority, impact, sentiment, and resolution time. |
| `raw/telkom_topology_config_change_logs.csv` | Site inventory snapshots, topology state, and the incident-triggering config change. |
| `processed/telkom_cell_degradation_incident_summary.csv` | Engineer-facing incident output with Facts, AI Inference, Recommendation, confidence, and benefit estimate. |

## How It Maps To The Expected Outcomes

1. **Flag significant issues out of noise:** `degradation_label`, `anomaly_score`, and `severity` identify the degraded cell and distinguish it from normal/noise events.
2. **Cluster related data into one incident:** all relevant rows carry `incident_id = INC-20260915-JHB-CBD-003-B`.
3. **Support RCA with evidence:** the summary file separates `observed_facts`, `ai_inference`, and `recommendation`.
4. **Measure benefit:** the summary estimates investigation time reduced from `75` to `18` minutes and duplicate alarm suppression of `83.3%`.

## Regeneration

The raw and processed files in this folder are the dataset. Seed `260916` is recorded in `dataset_manifest.json`. There is no generator script in the repo. To recompute detections, clusters, and the engineer report, run `notebooks/telkom_npm_poc_colab.ipynb` as described in the repo README. That notebook writes `*_colab` files here and leaves these files in place.
