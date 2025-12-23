# Incident Timeline – SSH Brute Force Attack

## Overview
This timeline reconstructs the SSH brute force incident observed on the Ubuntu endpoint monitored by Wazuh.

---

## Timeline of Events

- **T0** – Attacker initiates SSH brute force attempts
- **T1** – Multiple authentication failures detected
- **T2** – Successful SSH authentication observed
- **T3** – Privileged (`sudo`) command execution detected
- **T4** – Fail2Ban threshold exceeded
- **T5** – Attacker IP blocked
- **T6** – No further SSH authentication alerts observed

---

## Outcome

The incident was:
- Detected
- Investigated
- Contained
- Mitigated using automated controls
