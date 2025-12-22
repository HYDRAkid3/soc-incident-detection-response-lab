# Network Flow – SOC Lab

This document describes the network communication paths within the SOC lab environment and explains how traffic flows between components from an operational security perspective.

The network flow is designed to support **attack simulation, centralized detection, analyst investigation, and automated response**, while maintaining clear trust boundaries.

---

## Network Communication Matrix

| Source            | Destination          | Port(s)        | Protocol | Purpose |
|-------------------|----------------------|----------------|----------|---------|
| Kali Linux        | Ubuntu Endpoint      | 22             | TCP      | SSH brute force and authentication attempts |
| Ubuntu Endpoint   | Wazuh Manager        | 1514           | TCP      | Secure log and event forwarding |
| Ubuntu Endpoint   | Wazuh Authd          | 1515           | TCP      | Agent registration and authentication |
| Analyst Workstation | Wazuh Dashboard    | 443 (or 5601)  | HTTPS    | Alert visualization and threat hunting |
| Wazuh Manager     | Wazuh Indexer        | 9200           | HTTPS    | Event indexing and storage |
| Wazuh Dashboard   | Wazuh Manager API    | 55000          | HTTPS    | API queries and health checks |

---

## Traffic Flow Description

### 1. Attack Initiation
- Kali Linux initiates SSH connections to the Ubuntu endpoint over TCP port 22.
- This traffic represents untrusted external behavior targeting a monitored internal host.
- Both failed and successful authentication attempts are generated during this phase.

### 2. Endpoint Telemetry Generation
- The Ubuntu endpoint records SSH activity in system logs (`auth.log`, PAM, systemd).
- Privilege escalation events (sudo usage) are also logged if authentication succeeds.

### 3. Log Collection & Forwarding
- The Wazuh Agent on the Ubuntu endpoint continuously monitors system logs.
- Collected telemetry is securely forwarded to the Wazuh Manager over port 1514.
- Agent authentication and enrollment occur over port 1515 via Wazuh Authd.

### 4. Centralized Analysis
- The Wazuh Manager decodes incoming logs and applies detection rules.
- Events matching security rules generate alerts with severity levels and MITRE ATT&CK mappings.

### 5. Event Indexing
- Processed alerts and events are sent to the Wazuh Indexer.
- The indexer stores events for search, correlation, and historical analysis.

### 6. Analyst Visibility
- The Wazuh Dashboard queries indexed data and the Manager API.
- Analysts access the dashboard via HTTPS to perform:
  - Alert triage
  - Threat hunting
  - Timeline analysis
  - Response verification

---

## Security Perspective

- **Untrusted Zone:** Kali Linux attacker
- **Monitored Zone:** Ubuntu endpoint
- **Trusted SOC Zone:** Wazuh Manager, Indexer, and Dashboard

All detection is **host-based**, relying on endpoint telemetry rather than packet inspection.  
This design mirrors environments where network IDS is unavailable or limited.

---

## Key Ports Summary

- **22/TCP** – SSH (attack surface)
- **1514/TCP** – Wazuh Agent → Manager (log forwarding)
- **1515/TCP** – Wazuh Agent → Authd (enrollment)
- **443/TCP** – Analyst → Dashboard (secure access)
- **55000/TCP** – Dashboard → Manager API
- **9200/TCP** – Manager → Indexer (event storage)

---

## Notes

- Network flows are intentionally minimal to reduce noise and complexity.
- The focus is on **visibility and response**, not network segmentation.
- In production environments, additional controls such as firewalls, VPNs, and network IDS would typically be implemented.

