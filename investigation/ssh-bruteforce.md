# SSH Brute Force – SOC Investigation

## 🕵️ Analyst Objective
Investigate SSH authentication failures and confirm brute force activity.

---

## ⏱️ Timeline
- Repeated failed logins detected
- Source IP identified: `10.0.0.226`
- Successful login observed

---

## 🔍 Investigation Steps
1. Open Wazuh Dashboard
2. Navigate to Threat Hunting → Events
3. Filter:
   - `agent.name: ubuntu-endpoint1`
   - `rule.description: sshd authentication failed`

---

## 🚨 Findings
- Attack originated from Kali Linux VM
- Brute force behavior confirmed

---

## 🛡️ Recommendations
- Enable Fail2Ban
- Disable password-based SSH
- Enforce SSH key authentication
- Enable MFA
