# Trust Boundaries & Scope

This document defines trust assumptions and boundaries within the SOC lab environment.

---

## Trust Boundaries

- Kali Linux is considered untrusted and external.
- Ubuntu endpoint is an internal monitored system.
- Wazuh Manager, Indexer, and Dashboard are trusted SOC infrastructure.

---

## Assumptions

- Secure communication exists between Wazuh Agent and Manager.
- Credentials used in the lab are non-production.
- The lab simulates a single-host compromise scenario.

---

## Scope Limitations

- No lateral movement simulation.
- No malware execution or payload delivery.
- No network packet inspection or IDS.

These boundaries ensure clear analyst expectations and controlled detection scope.
