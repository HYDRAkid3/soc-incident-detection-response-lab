# SOC Lab Architecture

This document describes the architecture of the Mini SOC Lab built using Wazuh.

## Components Overview

### Attacker
- **Kali Linux**
- Used to simulate real-world attacks such as:
  - SSH brute-force attacks
  - Network port scanning

### Endpoint
- **Ubuntu Linux VM**
- Runs the **Wazuh Agent**
- Generates security telemetry including:
  - Authentication logs
  - Process execution
  - File integrity events
  - Privilege escalation activity

### SOC Platform
- **Wazuh Manager**
  - Receives logs from agents
  - Performs decoding and rule-based analysis
- **Wazuh Indexer (OpenSearch)**
  - Stores and indexes security events
- **Wazuh Dashboard**
  - Used by analysts for monitoring, threat hunting, and investigations

### Analyst
- Security analyst accesses alerts and events through the Wazuh Dashboard using a web browser.

## Data Flow

1. Attacks are launched from Kali Linux against the Ubuntu endpoint.
2. The Wazuh Agent on Ubuntu collects system and security logs.
3. Logs are securely forwarded to the Wazuh Manager.
4. Processed events are indexed in the Wazuh Indexer.
5. Alerts and logs are visualized in the Wazuh Dashboard for analysis.

