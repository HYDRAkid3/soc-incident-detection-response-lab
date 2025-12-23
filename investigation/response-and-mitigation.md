# Incident Response & Mitigation – SSH Brute Force

## Incident Summary

An SSH brute force attack was detected against the Ubuntu endpoint (`ubuntu-endpoint1`) originating from IP `10.0.0.226`.

Multiple failed authentication attempts were followed by:
- A successful SSH login
- Privileged (`sudo`) command execution

This confirms a **true security incident** rather than benign activity.

---

## Immediate Response Actions (Containment)

1. **Block Attacker IP**
   - Block `10.0.0.226` using Fail2Ban / firewall controls

2. **Terminate Active Sessions**
   - Identify and terminate any active SSH sessions from the attacker IP

3. **Credential Protection**
   - Reset credentials for affected accounts
   - Invalidate any active authentication sessions

---

## Short-Term Remediation

- Enable Fail2Ban with tuned thresholds
- Disable password-based SSH authentication
- Enforce key-based authentication
- Audit `sudo` and authentication logs

---

## Long-Term Mitigation & Hardening

- Implement MFA for SSH access
- Rotate credentials and SSH keys periodically
- Apply defense-in-depth controls
- Integrate threat intelligence enrichment

---

## Automation Opportunities

- Auto-block IPs triggering correlated SSH alerts
- Auto-escalate incidents with brute force + success patterns
- Auto-create incident tickets

---

## Residual Risk

SSH remains a high-value target.  
Continuous monitoring and detection tuning are required to maintain visibility while reducing alert fatigue.
