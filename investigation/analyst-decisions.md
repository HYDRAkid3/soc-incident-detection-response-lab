# Analyst Decision Log

## Why This Was Treated as an Incident

This activity met the criteria for a confirmed security incident due to:

- Repeated SSH authentication failures from a single external source
- Successful SSH login following multiple failures
- Privileged (`sudo`) activity immediately after authentication
- Clear mapping to MITRE ATT&CK technique **T1110 – Brute Force**

This behavior exceeds normal user error and indicates account compromise.

---

## Why Automated Response Was Appropriate

- Clear brute force behavior against a known attack surface (SSH)
- Low likelihood of false positives
- Host-based controls were available for immediate containment
- Automated blocking reduced risk of further compromise

---

## Escalation Decision

- **SOC-level escalation:** Required  
  (Incident grouping, investigation, and response)

- **Management / external escalation:** Not required  
  - Single endpoint affected
  - No lateral movement detected
  - Attacker contained successfully

---

## Final Analyst Verdict

Confirmed Security Incident  
Contained  
Residual risk reduced  
No further escalation required
