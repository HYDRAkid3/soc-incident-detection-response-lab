# Step-by-Step Build Guide (Complete Tutorial)

This guide walks you through building a **SOC Lab** from scratch that detects and investigates an **SSH brute-force attack** using **Wazuh**.

You will build the lab in this flow:

Kali Attacker → Ubuntu Endpoint → Wazuh Agent → Wazuh Manager/Indexer → Dashboard Investigation

This guide is written so that **a beginner can complete it successfully on the first attempt**.

For commands and installation steps, always use the **official documentation links provided**.

---

## Lab Architecture Overview

You will deploy three systems:

1. **Ubuntu Endpoint**
   - Victim system
   - Generates SSH authentication logs

2. **Wazuh Stack**
   - Central SOC platform
   - Collects logs, triggers alerts, enables investigation

3. **Kali Linux**
   - Attacker machine
   - Simulates reconnaissance and brute-force attacks

All systems must be able to communicate over the network.

---

## Step 1 – Prepare Virtual Machines and Networking

### What to do
- Create three virtual machines (VMware / VirtualBox / cloud):
  - Ubuntu Server (Endpoint)
  - Wazuh Server (Manager + Indexer + Dashboard)
  - Kali Linux (Attacker)
- Place all machines on the **same internal or host-only network**.

### Why this matters
- If networking is misconfigured, logs and alerts will never reach Wazuh.

### Verify
- Each system has an IP address
- Each system can reach the others (ping or port access)
- You can access the Wazuh server from your browser

### Official resources
- Ubuntu Server install: https://ubuntu.com/download/server
- Kali Linux install: https://www.kali.org/get-kali/
- VirtualBox networking: https://www.virtualbox.org/manual/ch06.html

---

## Step 2 – Deploy the Ubuntu Endpoint (Victim System)

### What to do
1. Install **Ubuntu Server**
2. Install and enable **OpenSSH Server**
3. Confirm authentication logging is enabled

### Why this matters
- SSH is a common real-world attack vector
- `/var/log/auth.log` is the primary evidence source

### Verify
- You can SSH into Ubuntu using valid credentials
- File `/var/log/auth.log` exists
- Failed login attempts appear in `auth.log`

### Official documentation
- OpenSSH Server on Ubuntu:  
  https://documentation.ubuntu.com/server/how-to/security/openssh-server/

---

## Step 3 – Establish a Clean Baseline on Ubuntu

### What to do
- Perform:
  - One successful SSH login
  - One failed SSH login
- Observe the log entries created

### Why this matters
- Baselines help distinguish attacks from normal behavior
- Enables accurate incident timelines later

### Verify
- Successful login entries exist in `auth.log`
- Failed login entries exist with:
  - Timestamp
  - Username
  - Source IP

---

## Step 4 – Deploy the Wazuh Stack (SOC Platform)

You may use **either** option below.

### Option A – Quickstart (Recommended for beginners)

### What to do
- Install Wazuh using the official quickstart installer

### Official documentation
- Wazuh Quickstart:  
  https://documentation.wazuh.com/current/quickstart.html

---

### Option B – Docker Deployment (Advanced)

### What to do
- Deploy Wazuh Manager, Indexer, and Dashboard using Docker

### Official documentation
- Wazuh Docker deployment:  
  https://documentation.wazuh.com/current/deployment-options/docker/

---

### Verify (for both options)
- Wazuh services are running
- Dashboard loads in browser
- No critical service errors

---

## Step 5 – Validate Wazuh Stack Stability

### What to do
- Log in to the dashboard
- Ensure the manager and indexer are healthy

### Why this matters
- Installing agents on a broken stack wastes time

### Verify
- Dashboard loads without errors
- Indexer is healthy
- Manager is ready to accept agents

---

## Step 6 – Install Wazuh Agent on Ubuntu Endpoint

### What to do
1. Install Wazuh agent on Ubuntu
2. Register the agent with the Wazuh Manager
3. Enable authentication log collection

### Why this matters
- The agent sends endpoint logs to the SOC platform

### Verify
- Ubuntu appears in Wazuh dashboard
- Agent status is **Active**
- SSH authentication logs are visible

### Official documentation
- Wazuh agent installation (Linux):  
  https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html
- Log collection configuration:  
  https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/

---

## Step 7 – Validate Log Ingestion (Pre-Attack Test)

### What to do
- Perform:
  - One successful SSH login
  - One failed SSH login
- Search for these events in Wazuh

### Why this matters
- Confirms ingestion before generating large attack traffic

### Verify
- Events appear in Wazuh
- Fields populated:
  - Source IP
  - Username
  - Timestamp

---

## Step 8 – Deploy Kali Linux Attacker

### What to do
- Install Kali Linux
- Ensure it can reach the Ubuntu endpoint

### Why this matters
- Kali generates realistic attack telemetry

### Verify
- Kali can reach Ubuntu SSH port
- Tools available: `nmap`, `hydra`

### Official documentation
- Kali installation guide:  
  https://www.kali.org/docs/installation/

---

## Step 9 – Reconnaissance Using Nmap

### What to do
- Scan the Ubuntu endpoint from Kali
- Identify open SSH service

### Why this matters
- Simulates real attacker behavior
- Establishes context for later attack

### Verify
- SSH port detected
- Scan timestamps recorded

### Official documentation
- Nmap reference:  
  https://nmap.org/book/man.html

---

## Step 10 – SSH Brute Force Attack Simulation

### What to do
- Run Hydra against Ubuntu SSH
- Use a small password list and controlled speed

### Why this matters
- Generates repeated authentication failures
- Triggers SOC detections

### Verify on Ubuntu
- Multiple failed login attempts in `auth.log`

### Verify in Wazuh
- SSH brute-force alerts generated
- Attacker IP clearly identified

### Official documentation
- Hydra tool (Kali):  
  https://www.kali.org/tools/hydra/
- Wazuh brute-force detection PoC:  
  https://documentation.wazuh.com/current/proof-of-concept-guide/detect-brute-force-attack.html

---

## Step 11 – SOC Investigation and Timeline Reconstruction

### What to do
- Correlate:
  - Kali attack timestamps
  - Ubuntu logs
  - Wazuh alerts
- Build a timeline

### Why this matters
- Demonstrates analyst-level investigation skills

### Verify
- You can answer:
  - Who attacked?
  - From which IP?
  - Which account was targeted?
  - When did the attack start and stop?

---

## Step 12 – Optional: Automatic Response (Advanced)

### What to do
- Enable Wazuh Active Response to block attacker IP

### Why this matters
- Adds response capability, not just detection

### Official documentation
- Active Response for SSH brute force:  
  https://documentation.wazuh.com/current/user-manual/capabilities/active-response/ar-use-cases/blocking-ssh-brute-force.html

---

## Step 13 – Documentation and Evidence

### What to capture
- Ubuntu `auth.log` screenshots
- Wazuh alerts
- Agent status
- Investigation views

### Final result
- A complete, reproducible SOC lab
- Ready for portfolio and interviews

---

## Final Outcome

If all steps are completed successfully:
- Endpoint telemetry flows correctly
- Attacks trigger alerts
- Investigation is possible end-to-end

This lab represents a **fully functional SOC detection and investigation environment**.
