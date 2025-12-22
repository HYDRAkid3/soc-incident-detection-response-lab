# SOC Lab Architecture Overview

This document provides a high-level overview of the SOC lab architecture and explains the design decisions behind each component.

---

## Architecture Design Philosophy

The SOC lab is intentionally designed to be:
- Minimal but realistic
- Host-based rather than network-heavy
- Analyst-focused rather than tool-focused

The goal is to simulate how a SOC operates when visibility is primarily derived from endpoint telemetry.

---

## Architectural Zones

### Attacker Zone
- Kali Linux represents an untrusted external entity.
- Generates malicious and reconnaissance traffic targeting exposed services.

### Monitored Zone
- Ubuntu endpoint acts as the protected asset.
- Runs a Wazuh Agent to provide continuous security telemetry.

### SOC Zone
- Wazuh Manager, Indexer, and Dashboard form the SOC backend.
- Responsible for detection, storage, and analyst visibility.

---

## Detection Strategy

- Detection is based on host-level logs rather than packet inspection.
- Authentication behavior, privilege escalation, and system activity form the primary detection signals.
- Alerts are generated using rule-based analysis mapped to MITRE ATT&CK.

---

## Response Strategy

- Automated containment is implemented using Fail2Ban.
- SSH brute force behavior triggers temporary IP blocking.
- Post-response validation confirms alert suppression.

---

## Design Tradeoffs

- Network IDS/IPS is intentionally excluded to maintain scope.
- Focus is placed on analyst reasoning and response validation.
- Architecture mirrors environments with limited network visibility.

