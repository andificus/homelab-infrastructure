# Homelab Infrastructure

Documentation and design specs for a self-built homelab environment.
Covers network layout, server roles, backup strategy, monitoring, and security.

Built as both a learning environment and a reference for real-world IT architecture decisions.

---

## 📁 Structure

| Folder | Purpose |
|---|---|
| `Network/` | Network diagram, VLAN layout, firewall rules |
| `Servers/` | Server roles, specs, and OS details |
| `Backup/` | Backup strategy and retention policy |
| `Monitoring/` | Monitoring setup and alerting |
| `Security/` | Security hardening and access control |

---

## 🧠 Design Goals

- Simulate a small business environment
- Practice real-world infrastructure concepts
- Document everything as if handing off to another engineer
- Keep it affordable and expandable

---

## 🖥️ Environment Overview

| Component | Details |
|---|---|
| Hypervisor | Proxmox VE |
| Domain Controller | Windows Server 2022 |
| DNS / DHCP | pfSense |
| File Server | Windows Server 2022 |
| Monitoring | Grafana + Prometheus |
| Backup | Veeam Community Edition |
| Workstation | Windows 11 Pro |

---

## 📌 Quick Links

- [Network Design](./Network/network-design.md)
- [Server Roles](./Servers/server-roles.md)
- [Backup Strategy](./Backup/backup-strategy.md)
- [Monitoring Setup](./Monitoring/monitoring-setup.md)
- [Security Hardening](./Security/security-hardening.md)