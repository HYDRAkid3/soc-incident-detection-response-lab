# 🔐 SSH Brute Force Attack – Simulation

This document describes a simulated SSH brute force attack executed within the SOC lab environment.  
The scenario is designed to generate authentication-related telemetry and validate detection, investigation, and alerting capabilities in **Wazuh**.

> ⚠️ **Disclaimer**  
> This activity was conducted in an isolated lab environment for **educational and defensive security purposes only**.

---

## 1. Objective

- Simulate credential brute force activity against an SSH service  
- Generate multiple failed SSH authentication attempts  
- Achieve a successful SSH login  
- Validate Wazuh detection rules and MITRE ATT&CK mapping  
- Produce telemetry suitable for SOC investigation workflows  

---

## 2. Environment Overview

| Role            | Operating System | IP Address    | Notes                                  |
|-----------------|------------------|---------------|----------------------------------------|
| Attacker        | Kali Linux       | 10.0.0.226    | Untrusted external attacker machine    |
| Target / Victim | Ubuntu Linux     | 10.0.0.95     | Monitored endpoint with Wazuh Agent    |

**Target Service**
- Service: OpenSSH  
- Port: 22  

---

## 3. Tools Used

- Kali Linux  
- THC-Hydra  
- Nmap  
- OpenSSH  
- Wazuh (Agent, Manager, Indexer, Dashboard)  

---

## 4. Attack Phases

### 4.1 Reconnaissance

The attacker first verified SSH service availability on the target system.

```bash
nmap -p 22 10.0.0.95
