# Attack Scenarios

This directory documents **simulated adversary activity** executed against the Mini SOC Lab environment.

Each attack scenario is intentionally designed to:
- Generate **realistic security telemetry**
- Validate **detection, investigation, and alerting** workflows
- Mirror **real-world SOC use cases** rather than theoretical attacks

All scenarios are executed in a **controlled and isolated lab environment** and are **fully reproducible**.

---

## Purpose of Attack Scenarios

The goals of this directory are to:

- Emulate common attacker techniques observed in production environments
- Produce log and alert data suitable for SOC analysis
- Demonstrate how attacks progress across multiple phases (recon → access)
- Support downstream documentation such as:
  - Detection logic
  - Threat hunting
  - Incident investigation
  - MITRE ATT&CK mapping

Each scenario focuses on **signal quality over quantity** — fewer attacks, documented deeply.

---

## Available Attack Scenarios

### 1. SSH Brute Force Attack

**Description**  
Simulates a credential brute force attack against an exposed SSH service on a Linux endpoint.

**Key Behaviors Simulated**
- Service discovery of SSH
- Repeated authentication failures
- Successful login following brute force attempts

**Telemetry Generated**
- SSH authentication failure events
- Successful SSH login events
- Host-based authentication logs
- Wazuh alerts mapped to MITRE ATT&CK

**SOC Capabilities Validated**
- Host-based log collection
- Authentication anomaly detection
- Alert correlation and visualization
- Threat hunting via Wazuh Dashboard

📄 Detailed documentation:  
- `ssh-bruteforce.md`

---

## Notes

- All attack scenarios are **non-destructive**
- No real credentials or production systems are involved
- Scenarios are designed to be **extendable** as new detections or defenses are added

Future attack scenarios may be added following the same structure and documentation standard.
