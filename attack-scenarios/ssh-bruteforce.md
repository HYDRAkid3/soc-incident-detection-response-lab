# SSH Brute Force Attack – Simulation

## 🎯 Objective
Simulate an SSH brute force attack from Kali Linux against a monitored Ubuntu endpoint to generate authentication failure events and validate Wazuh detections.


## 🛠️ Tools Used
- Kali Linux
- THC-Hydra
- Nmap
- OpenSSH


## 🧠 Attack Description
The attacker performed a credential brute force attack against the SSH service running on the Ubuntu endpoint. Multiple failed login attempts were generated, followed by a successful authentication.


## 👨‍💻 Attacker Details
- VM: Kali Linux
- IP: `10.0.0.226`


## 🎯 Target Details
- VM: Ubuntu Endpoint
- IP: `10.0.0.95`
- Service: SSH (22)


## 🔍 Reconnaissance
```bash
nmap -p 22 10.0.0.95

Result: SSH service discovered open.

## Brute Force Execution
hydra -l ubuntu -P passwords.txt ssh://10.0.0.95

Outcome:
1. Multiple failed authentication attempts
2. One successful login

## 🧩 MITRE ATT&CK Mapping
T1110 – Brute Force

## 📸 Evidence
https://github.com/HYDRAkid3/mini-soc-lab/blob/main/screenshots/nmap_scan_ubuntu.png
https://github.com/HYDRAkid3/mini-soc-lab/blob/main/screenshots/hydra_bruteforce.png

