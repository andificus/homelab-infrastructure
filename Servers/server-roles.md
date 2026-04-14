# Server Roles

## Overview
All servers run as virtual machines on a Proxmox hypervisor.
Each VM is assigned a dedicated role to mirror a real small business environment.

---

## VM Inventory

| VM Name | OS | Role | IP Address | VLAN |
|---|---|---|---|---|
| DC01 | Windows Server 2022 | Domain Controller, DNS, DHCP | 10.0.20.10 | Servers |
| FS01 | Windows Server 2022 | File Server | 10.0.20.11 | Servers |
| MON01 | Ubuntu 22.04 | Monitoring (Grafana + Prometheus) | 10.0.20.12 | Servers |
| BACKUP01 | Windows Server 2022 | Backup Server (Veeam) | 10.0.20.13 | Servers |
| WS01 | Windows 11 Pro | Workstation (test client) | 10.0.30.10 | Workstations |

---

## Role Details

### DC01 — Domain Controller
- Runs Active Directory Domain Services (ADDS)
- Hosts DNS for the lab.local domain
- Manages Group Policy Objects (GPOs)
- Primary authentication source for all domain-joined machines

### FS01 — File Server
- Hosts shared folders for department simulation
- NTFS permissions mirror real business structure
- Folders: IT, HR, Finance, General
- Shadow copies enabled for basic file recovery

### MON01 — Monitoring Server
- Prometheus scrapes metrics from all VMs
- Grafana dashboards for CPU, RAM, disk, and network
- Alerting configured for high CPU and low disk space
- Runs on Ubuntu to simulate mixed OS environments

### BACKUP01 — Backup Server
- Veeam Community Edition for VM backups
- Daily backups of DC01 and FS01
- Retention policy: 7 daily, 4 weekly
- Backup jobs logged and verified automatically

### WS01 — Workstation
- Domain joined test client
- Used to validate GPOs, login scripts, and mapped drives
- Simulates end user environment

---

## Proxmox Host Specs

| Component | Details |
|---|---|
| CPU | Intel Core i5 (6 core) |
| RAM | 32GB DDR4 |
| Storage | 1TB NVMe (VMs) + 2TB HDD (backups) |
| Network | 2x 1GbE NICs |
| OS | Proxmox VE 8.x |