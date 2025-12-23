#  Tool Selection & Design Rationale

A good SOC lab is not about using the most expensive tools.
It’s about choosing tools that **teach you how SOCs actually work**.

This section explains why each component was chosen.

---

##  Why Ubuntu Linux (Monitored Endpoint)

Ubuntu Linux is one of the most widely used Linux distributions in:
- Cloud environments
- Enterprise servers
- Developer infrastructure

### Why it works well for a SOC lab:
- Produces rich authentication logs (`/var/log/auth.log`)
- Common SSH exposure
- Realistic user and privilege model
- Lightweight and stable

Ubuntu allows you to practice:
- SSH attack detection
- Privilege escalation monitoring
- Log-based investigations

Official site:  
https://ubuntu.com/

---

##  Why Kali Linux (Attacker Machine)

Kali Linux is the **industry standard offensive security distribution**.

It is widely used by:
- Penetration testers
- Red teamers
- Security researchers
- Adversary emulation teams

### Why Kali is ideal here:
- Comes pre-installed with tools like:
  - Nmap (reconnaissance)
  - Hydra (brute force)
- Reduces setup overhead
- Produces realistic attack patterns

In a SOC context, Kali represents:
> “What real attackers might look like, not what textbooks show.”

Official site:  
https://www.kali.org/

---

##  Why Wazuh (SOC Platform)

Wazuh is a **powerful open-source SIEM + EDR platform**.

### Why Wazuh is an excellent SOC learning tool:
- Agent-based telemetry collection
- Real-time alerting
- MITRE ATT&CK mapping
- File integrity monitoring
- Authentication and process visibility

Most importantly:
> Wazuh teaches **how detection works**, not just how dashboards look.

### Why not Splunk / Sentinel?
- Licensing cost is prohibitive
- Hard to replicate full pipelines in home labs
- Less transparent for beginners

Wazuh provides **enterprise-grade visibility without barriers**.

Official site:  
https://wazuh.com/

---

##  Design Philosophy

Every tool in this lab was chosen to answer one question:

> “What would a SOC analyst realistically see, investigate, and respond to?”

That philosophy guides the entire project.
