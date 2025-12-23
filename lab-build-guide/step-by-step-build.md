# 🛠️ Step-by-Step Build

## Phase 1 – Deploy Ubuntu Endpoint
- Install Ubuntu Server
- Enable SSH
- Create test users
- Verify logging (`/var/log/auth.log`)

## Phase 2 – Deploy Wazuh Stack
- Install Wazuh Manager, Indexer, Dashboard
- Validate services
- Access dashboard

## Phase 3 – Install Wazuh Agent
- Register Ubuntu endpoint
- Confirm log ingestion

## Phase 4 – Deploy Kali Attacker
- Install Kali Linux
- Verify Hydra and Nmap availability

## Phase 5 – Validate Telemetry
- Generate failed SSH attempts
- Confirm alerts appear in Wazuh
