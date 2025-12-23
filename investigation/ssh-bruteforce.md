# SSH Brute Force – SOC Investigation

## 🕵️ Analyst Objective
Investigate SSH authentication alerts to determine whether activity represents a brute force attack or benign behavior.

---

## ⏱️ Timeline Summary
- Repeated SSH authentication failures detected
- Source IP identified: `10.0.0.226`
- Successful SSH authentication observed
- Privileged activity (`sudo`) detected shortly after

---

## 🔍 Investigation Steps

1. Open Wazuh Dashboard
2. Navigate to **Threat Hunting → Events**
3. Apply filters:
   - `agent.name: ubuntu-endpoint1`
   - `rule.description: sshd authentication failed`

4. Review authentication success and privilege escalation events
5. Correlate activity by source IP and timestamp

---

## 🚨 Findings

- Attack originated from Kali Linux attacker VM
- High-volume authentication failures observed
- Successful SSH login followed by immediate privilege escalation
- No evidence of lateral movement

This confirms brute force activity resulting in account compromise.

---

## 🛡️ Analyst Recommendations

- Enforce Fail2Ban for SSH
- Disable password-based authentication
- Require SSH key-based access
- Enable MFA where possible
- Monitor for post-authentication privilege escalation
