# Linux Auditd Record Types Reference

A structured, curated reference dataset of Linux Audit framework (`auditd` / kernel audit subsystem) event types, numeric record identifiers, origin scopes, operational classes, and functional categories.

---

## 📌 Overview

The Linux Audit subsystem generates structured security event logs for system calls, authentication attempts, mandatory access control (MAC/SELinux/AppArmor) events, daemon operations, integrity monitoring, and kernel anomalies.

This dataset provides a unified mapping of **221 audit record types** across kernel headers and distribution reference documentation to support:
- Security Operations Center (SOC) and detection engineering
- SIEM field parsing and event enrichment (Splunk, Elastic)
- Rule development for Linux host monitoring (e.g., Sigma, Auditbeat, Osquery)

---

## 📊 Dataset Summary

| Metric | Count | Details |
| :--- | :--- | :--- |
| **Total Record Types** | `221` | Numeric IDs spanning `1000` to `2507` |
| **Origin Subsystems** | `2` | `USER` (134), `KERN` (87) |
| **Operational Classes** | `6` | `IND` (125), `SC` (67), `CTL` (14), `DEP` (12), `SC/IND` (2), `IND/SC` (1) |
| **Functional Categories** | `14` | Grouped from trusted apps to virtualization events |

---

## 📂 File Schema (`auditd_record_types.csv`)

The dataset contains exactly 7 columns:

| Column | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `record_id` | Integer | Unique numeric identifier for the audit event type | `1300`, `1100` |
| `type_name` | String | Standard record type name (used in `/var/log/audit/audit.log`) | `SYSCALL`, `USER_AUTH` |
| `macro_name` | String | Linux kernel C macro definition | `AUDIT_SYSCALL` |
| `origin` | String | Generation space: `USER` (user space) or `KERN` (kernel space) | `KERN` |
| `class` | String | Event class: `IND` (Independent), `SC` (System call), `CTL` (Control), `DEP` (Dependent) | `SC` |
| `category` | String | High-level functional category name | `Kernel audit event records` |
| `description` | String | Human-readable explanation of the record's meaning and purpose | `System call audit record.` |

---


## 🏷️ Operational Classes

- **`CTL` (Control):** System management messages (e.g., enable/disable auditing, buffer rate limits). Often filtered from log output by the daemon.
- **`IND` (Independent):** Self-contained single-line records emitted immediately when an action occurs (common in user space authentication/daemons).
- **`SC` (System Call):** Kernel-level records emitted during system call execution; usually correlated with `SYSCALL`

---

## 🤝 Contributing

Contributions to improve descriptions, add newly introduced Linux kernel audit macros, or clarify subsystem behaviors are welcome:

1. Fork this repository.
2. Create a feature branch (git checkout -b update-macro-definitions).
3. Commit your changes and open a Pull Request.

---

## ⚖️ License & Disclaimer

- **License:** The compiled CSV structure and documentation are provided under the MIT License. Upstream Linux kernel constants and macro names are subject to their respective kernel and distribution licensing terms.
- **Disclaimer:** Field behaviors, availability, and logging formats may vary depending on the Linux distribution, kernel compilation flags, and auditd configuration.
