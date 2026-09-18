# Engineer Incident Report

## Ranked Incidents

### CL-0001 - JHB-CBD-003-B

- Site: `JHB-CBD-003`
- Window: `2026-09-15T08:00` to `2026-09-15T14:45`
- Raw events clustered: `131`
- Predicted root cause: `Transport backhaul congestion`
- Confidence: `1.0`

#### Facts

- Cell JHB-CBD-003-B was detected as degraded between 2026-09-15T08:00 and 2026-09-15T14:45.
- Worst detection score was 100 with severity critical.
- Accessibility reached 83.29% versus rolling baseline 96.39%.
- Downlink throughput was 4.22 Mbps versus rolling baseline 34.61 Mbps.
- The cluster contains 7 alarms, 47 complaints, 54 drive-test samples, and 2 topology/config records.
- Relevant topology/config evidence includes CFG-20260915-04521: Protection route preference changed from fiber primary to microwave secondary during planned maintenance

#### AI Inference

- The evidence pattern most strongly matches `Transport backhaul congestion` with score `100.0`.
- Microwave transport degradation or CRC alarms are active.
- S1-U packet loss alarm indicates user-plane transport impairment.
- Packet loss is above the 2% operational threshold.
- Transport discard counters are elevated.
- A recent topology/config change exists before or during the degradation window.

#### Recommendation

- Check the serving transport path, validate microwave/fiber health, review recent protection-path changes, and monitor packet loss, discard counters, RRC failures, and complaint rate after correction.
