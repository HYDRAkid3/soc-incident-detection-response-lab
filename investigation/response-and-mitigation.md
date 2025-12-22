# Incident Response & Mitigation – SSH Brute Force

## Incident Summary
An SSH brute force attack was detected against the Ubuntu endpoint (`ubuntu-endpoint1`) originating from IP `10.0.0.226`. Multiple failed authentication attempts were followed by a successful login and privileged activity.

This indicates a confirmed security incident rather than benign noise.

---

## Immediate Response Actions (Containment)

1. **Block Attacker IP**
   - Temporarily block `10.0.0.226` at the host firewall (UFW / iptables).
   - If applicable, block at the network perimeter (router / security group).

2. **Terminate Active Sessions**
   - Identify active SSH sessions from the attacker IP.
   - Force logout of compromised sessions.

3. **Credential Protection**
   - Reset credentials for the affected user account.
   - Invalidate any active authentication tokens.

---

## Short-Term Remediation

1. **Enable Account Lockout Controls**
   - Deploy Fail2Ban for SSH to automatically block repeated failed attempts.
   - Configure thresholds (e.g., 5 failures in 5 minutes).

2. **Harden SSH Configuration**
   - Disable password-based authentication.
   - Enforce key-based authentication only.
   - Restrict SSH access to trusted IP ranges if possible.

3. **Audit Privileged Activity**
   - Review `sudo` and `auth` logs for unauthorized changes.
   - Verify no persistence mechanisms were introduced.

---

## Long-Term Mitigation & Hardening

- Implement Multi-Factor Authentication (MFA) for SSH.
- Rotate SSH keys periodically.
- Move SSH to a non-default port (defense-in-depth).
- Enable centralized logging and alert escalation.
- Integrate threat intelligence enrichment for attacker IPs.

---

## Automation Opportunities

- Auto-block IPs triggering correlated SSH alerts.
- Auto-create incident tickets for brute force + success patterns.
- Alert escalation when failed attempts transition into success.

---

## Residual Risk

Even with mitigations applied, SSH remains a high-value target. Continuous monitoring and alert tuning are required to reduce alert fatigue while maintaining detection fidelity.
