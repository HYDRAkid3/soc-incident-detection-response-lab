# 🖥️ Lab Environment Overview

This section describes the **overall lab environment**, not step-by-step commands.

Understanding the environment matters more than blindly installing tools.

---

## 🧱 High-Level Architecture

The lab consists of **three logical roles**:

1. Attacker
2. Endpoint
3. SOC Platform

Each role has a clear purpose and trust boundary.

---

## 💻 Host System Requirements

Recommended minimum:
- 16 GB RAM (8 GB may work with constraints)
- 50+ GB free disk space
- Hardware virtualization enabled

Virtualization platforms:
- VirtualBox
- VMware Workstation / Fusion

---

## 🖥️ Virtual Machines

| Role | Operating System | Purpose |
|----|----|----|
| Attacker | Kali Linux | Simulate adversary activity |
| Endpoint | Ubuntu Server | Target system |
| SOC | Wazuh Stack | Detection & investigation |

---

## 🌐 Networking Model

Recommended setup:
- Internal / Host-only network

Why?
- Prevents exposure to the internet
- Keeps attacks contained
- Mimics internal enterprise networks

All attack traffic, logs, and alerts remain **inside the lab**.

---

## 🧠 Key Principle

Do not rush setup.

Before moving on, always ask:
- Is telemetry flowing?
- Are timestamps correct?
- Can I explain this architecture to someone else?

If you can explain it, you understand it.
