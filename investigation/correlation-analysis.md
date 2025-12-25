# Correlation Analysis – SSH Brute Force Incident

## Why Correlation Matters

A single `sshd: authentication failed` alert is common and often benign.  
SOC analysts must identify **patterns**, not isolated alerts.

This incident demonstrates how multiple low-to-medium severity alerts combine into a **high-confidence security incident**.

---

## Observed Alert Chain

1. **Multiple SSH authentication failures**
   - Rule: `sshd: authentication failed`
   - Severity: Medium (Level 5)

2. **Successful SSH login**
   - Indicates password guessing or credential compromise

3. **Privileged activity detected**
   - `Successful sudo to ROOT executed`
   - Confirms attacker escalation

---

## Correlated Incident Narrative

- Brute force activity originated from `10.0.0.226`
- High frequency of failed SSH logins in a short time window
- Eventual successful authentication
- Immediate privileged command execution

This sequence confirms **account compromise**, not user error.

---

## SOC Incident Grouping Logic

| Signal | Individually | Correlated |
|------|-------------|------------|
| SSH failed login | Low | Medium |
| SSH success | Medium | High |
| Sudo activity | Medium | Critical |

---

## Analyst Decision

Confirmed Incident  
Not a false positive  
SOC-level escalation required

---

## Improvement Opportunity

Implement correlation rules that raise high-severity alerts when:
- Multiple SSH failures occur **AND**
- A successful login follows within a defined time window
