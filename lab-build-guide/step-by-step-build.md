# 🛠️ Step-by-Step Build (Conceptual)

This section outlines **what to build and verify**, not command-by-command instructions.

For installation commands, always refer to **official documentation**.

---

## Phase 1 – Deploy Ubuntu Endpoint

Goals:
- A reachable Linux system
- SSH enabled
- Logging verified

Validation checklist:
- SSH access works
- `/var/log/auth.log` exists
- Failed login attempts are logged

---

## Phase 2 – Deploy Wazuh Stack

Goals:
- Wazuh Manager running
- Indexer operational
- Dashboard accessible

Validation checklist:
- All services running
- Dashboard loads
- No critical service errors

---

## Phase 3 – Install Wazuh Agent on Ubuntu

Goals:
- Endpoint registered with Wazuh
- Log ingestion confirmed

Validation checklist:
- Agent appears in dashboard
- SSH logs visible
- Alerts begin triggering on failed attempts

---

## Phase 4 – Deploy Kali Attacker

Goals:
- Attack tooling available
- Network connectivity confirmed

Validation checklist:
- Kali can reach Ubuntu
- Nmap scans succeed
- Hydra runs as expected

---

## Phase 5 – Telemetry Validation

Goals:
- Confirm full SOC pipeline works

Validation checklist:
- Attack → log → alert flow verified
- Timeline reconstruction possible
- Analyst investigation feasible

If this phase works, your SOC lab is **ready**.
