# Detections

This directory documents the **detection logic, alert behavior, and analysis context**
used to identify malicious activity within the Mini SOC Lab.

The purpose of this section is to demonstrate how raw security telemetry
is transformed into **actionable alerts** aligned with SOC workflows.

Detections in this lab are based on:
- Host-based log analysis
- Rule-driven alerting
- MITRE ATT&CK alignment
- Analyst-oriented interpretation

---

## Scope of Detections

The detections documented here focus on:

- SSH authentication abuse
- Credential brute force behavior
- Failed-to-success login patterns
- Signal quality and alert tuning

Each detection corresponds directly to an **attack scenario**
documented in the `attack-scenarios/` directory.

---

## Detection Philosophy

This lab intentionally uses **default Wazuh rules** as a baseline
to illustrate:

- What is detected out-of-the-box
- Where noise exists
- How detections can be improved through tuning and correlation

Detection engineering is treated as an **iterative process**, not a static rule set.
