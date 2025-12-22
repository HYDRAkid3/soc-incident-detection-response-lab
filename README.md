# SOC Lab Architecture

This document describes the architecture and operational design of a Security Operations Center (SOC) lab built using Wazuh. The lab is designed to simulate a realistic end-to-end SOC workflow, covering attack execution, detection, investigation, and automated response.

---

## Architecture Goals

The primary goals of this architecture are to:

- Simulate a real-world attacker targeting a Linux endpoint
- Collect host-based security telemetry from the endpoint
- Detect malicious behavior using centralized log analysis
- Enable analyst-driven investigation through a SIEM-style dashboard
- Demonstrate automated containment using response controls

The architecture emphasizes **signal quality, analyst reasoning, and response validation**, rather than tool sprawl or excessive attack scenarios.

---

## Components Overview

### Attacker

- **Kali Linux**
- Represents an untrusted external adversary
- Used to simulate attack techniques including:
  - SSH brute force attacks
  - Network reconnaissance and port scanning

---

### Endpoint

- **Ubuntu Linux Virtual Machine**
- Runs the **Wazuh Agent**
- Acts as the monitored asset within the environment

#### Telemetry & Log Sources

The endpoint generates and forwards the following security-relevant telemetry:

- `/var/log/auth.log` – SSH authentication successes and failures
- PAM logs – Login and session activity
- sudo logs – Privilege escalation events
- systemd journal – Service execution and system-level events

This telemetry forms the foundation for detection, investigation, and response.

---

### SOC Platform

#### Wazuh Agent
- Installed on the Ubuntu endpoint
- Collects and forwards logs securely to the SOC backend

#### Wazuh Manager
- Central analysis engine
- Performs log decoding, rule matching, and alert generation
- Correlates events across time and context

#### Wazuh Indexer (OpenSearch)
- Stores and indexes processed security events
- Enables efficient searching and historical analysis

#### Wazuh Dashboard
- Web-based interface for SOC analysts
- Used for monitoring, threat hunting, alert review, and investigation
- Provides MITRE ATT&CK mapping and event visualization

---

### Analyst

- A SOC analyst accesses alerts and events through the Wazuh Dashboard
- Responsible for:
  - Alert triage
  - Event correlation
  - Incident classification
  - Validation of response effectiveness

---

## Trust Boundaries & Assumptions

- Kali Linux is treated as an untrusted external attacker
- The Ubuntu endpoint is an internal monitored host
- Secure communication is assumed between Wazuh Agent and Manager
- Wazuh Manager, Indexer, and Dashboard are trusted SOC infrastructure
- This lab focuses on **host-based detection** and does not include network IDS/IPS

These assumptions clearly define the detection scope and analyst expectations.

---

## Data Flow

1. Attacks are initiated from the Kali Linux attacker against the Ubuntu endpoint.
2. The Wazuh Agent on the Ubuntu system collects authentication, process, and privilege-related logs.
3. Logs are securely forwarded to the Wazuh Manager.
4. The Wazuh Manager analyzes events using predefined detection rules.
5. Processed events are indexed by the Wazuh Indexer.
6. Alerts and logs are visualized in the Wazuh Dashboard for analyst review.

---

## Operational Flow (SOC Perspective)

From a SOC analyst’s perspective, the workflow is as follows:

1. SSH authentication failures trigger security alerts.
2. The analyst reviews alert context in the Wazuh Dashboard.
3. Related events are correlated to identify brute force behavior.
4. A successful login following repeated failures increases severity.
5. Privileged activity (`sudo`) confirms potential compromise.
6. Automated response mechanisms (Fail2Ban) are triggered.
7. SSH access is blocked and further attempts are denied.
8. Post-containment verification confirms alert suppression.

This mirrors a real-world SOC detect → investigate → respond → verify lifecycle.

---

## Out of Scope

The following areas are intentionally excluded to maintain focus:

- Network packet inspection (IDS/IPS)
- Malware sandboxing
- Email security monitoring
- SOAR ticketing integrations

---

## Architecture Diagram

![SOC Architecture](https://github.com/HYDRAkid3/mini-soc-lab/blob/main/architecture/architecture_diagram.png)
