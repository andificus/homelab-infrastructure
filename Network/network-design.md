# Network Design

## Overview
The homelab network is segmented into VLANs to simulate a small business
environment. pfSense handles routing, DHCP, and firewall rules between segments.

---

## Network Diagram

    Internet
        |
    [ISP Modem]
        |
    [pfSense Firewall/Router]
        |
    [Managed Switch]
        |
        |--- VLAN 10 — Management
        |--- VLAN 20 — Servers
        |--- VLAN 30 — Workstations
        |--- VLAN 40 — IoT / Lab

---

## VLAN Layout

| VLAN ID | Name | Subnet | Purpose |
|---|---|---|---|
| 10 | Management | 10.0.10.0/24 | Hypervisor, switch, firewall management |
| 20 | Servers | 10.0.20.0/24 | Domain controller, file server, DNS |
| 30 | Workstations | 10.0.30.0/24 | End user machines |
| 40 | IoT / Lab | 10.0.40.0/24 | Isolated lab and IoT devices |

---

## Firewall Rules Summary

| From | To | Action | Reason |
|---|---|---|---|
| Workstations | Servers | Allow | Normal business traffic |
| Workstations | Management | Deny | No end user access to mgmt |
| IoT / Lab | All | Deny | Isolated by default |
| Management | All | Allow | Admin access |

---

## DNS / DHCP

- DNS: Handled by pfSense, forwarding to 1.1.1.1 and 8.8.8.8
- DHCP: pfSense assigns addresses per VLAN
- Internal Domain: lab.local

---

## Hardware

| Device | Role | Notes |
|---|---|---|
| Mini PC (Intel N100) | pfSense firewall | 4 NIC passthrough |
| Managed Switch | VLAN trunking | 802.1Q support |
| Proxmox Host | Hypervisor | Runs all VMs |