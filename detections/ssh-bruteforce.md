# SSH Brute Force Detection – Wazuh

## 🛡️ Detection Overview

This detection identifies repeated SSH authentication failures
consistent with a credential brute force attack.

The activity was generated during a controlled attack simulation
and detected using default Wazuh SSH authentication rules.

---

## 📊 Detection Source

- **Agent:** ubuntu-endpoint1
- **Monitored File:** `/var/log/auth.log`
- **Service:** sshd
- **Log Type:** Authentication events

---

## 🚨 Triggered Wazuh Rules

| Rule ID | Description                         | Level |
|--------:|-------------------------------------|------:|
| 5760    | sshd: authentication failed         | 5     |
| 5501    | PAM: login session opened           | 3     |
| 5502    | PAM: login session closed           | 3     |

These rules collectively indicate repeated failed login attempts
and subsequent successful authentication activity.

---

## 📄 Sample Alert (Sanitized)

```json
{
  "rule": {
    "id": "5760",
    "level": 5,
    "description": "sshd: authentication failed"
  },
  "agent": {
    "name": "ubuntu-endpoint1",
    "ip": "10.0.0.95"
  },
  "source": {
    "ip": "10.0.0.226"
  }
}
