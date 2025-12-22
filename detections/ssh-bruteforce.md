# SSH Brute Force Detection – Wazuh

## 🛡️ Detection Overview
Wazuh detected repeated SSH authentication failures indicating a brute force attack.

---

## 📊 Detection Source
- Agent: `ubuntu-endpoint1`
- Log File: `/var/log/auth.log`
- Service: SSHD

---

## 🚨 Triggered Rules

| Rule ID | Description                     | Level |
|-------|---------------------------------|-------|
| 5760  | sshd: authentication failed     | 5     |
| 5501  | PAM login session opened        | 3     |
| 5502  | PAM login session closed        | 3     |

---

## 📄 Sample Alert
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


## Severiy
Medium (Level 5) – repeated authentication failures from single source.

## 📸 Evidence
screenshots/wazuh_ssh_failed_events.png
