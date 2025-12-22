SSH Brute Force Attack Simulation
📌 Overview

This lab simulates an SSH brute force attack from a Kali Linux attacker machine against a monitored Ubuntu endpoint.
The purpose of this exercise is to generate authentication failure and success events and validate Wazuh detection and alerting within a controlled environment.

⚠️ Disclaimer:
This simulation was conducted in an isolated lab environment for educational and defensive security purposes only.

🎯 Objective

Simulate an SSH brute force attack

Generate multiple failed authentication attempts

Achieve a successful login

Validate Wazuh alerts and MITRE ATT&CK mapping

🛠️ Tools Used

Kali Linux

THC-Hydra

Nmap

OpenSSH

Wazuh (Monitoring & Detection)

🧠 Attack Scenario

The attacker performed a credential brute force attack against the SSH service running on the Ubuntu endpoint.
The attack resulted in:

Multiple failed SSH authentication attempts

One successful SSH login

Corresponding security alerts generated on the Wazuh manager

👨‍💻 Attacker Details

Machine: Kali Linux VM

IP Address: 10.0.0.226

🎯 Target Details

Machine: Ubuntu Endpoint VM

IP Address: 10.0.0.95

Service: SSH

Port: 22

🔍 Reconnaissance

The SSH service was identified using Nmap:

nmap -p 22 10.0.0.95


Result:

SSH service discovered running on port 22

🚀 Brute Force Execution

A credential brute force attack was launched using THC-Hydra:

hydra -l ubuntu -P passwords.txt ssh://10.0.0.95

Outcome

Multiple failed authentication attempts detected

One successful SSH login

Events forwarded and logged by Wazuh

📊 Detection & Logging

Failed and successful SSH login attempts were captured by the Ubuntu endpoint

Logs were forwarded to the Wazuh manager

Alerts were generated correlating with brute force behavior

🧩 MITRE ATT&CK Mapping

T1110 – Brute Force

📸 Evidence

Screenshots from the lab execution:

🔎 Nmap SSH Scan
https://github.com/HYDRAkid3/mini-soc-lab/blob/main/screenshots/nmap_scan_ubuntu.png

🔐 Hydra Brute Force Attack
https://github.com/HYDRAkid3/mini-soc-lab/blob/main/screenshots/hydra_bruteforce.png

✅ Conclusion

This lab successfully demonstrated how SSH brute force attacks generate detectable authentication patterns.
Wazuh effectively identified and logged the attack activity, validating its usefulness for SOC monitoring and threat detection.
