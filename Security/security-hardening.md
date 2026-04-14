# Security Hardening

## Overview
Security in the homelab is designed to mirror real small business best practices.
The goal is to minimize attack surface, enforce least privilege, and maintain
visibility into what is happening across the environment.

---

## Network Security

| Control | Implementation |
|---|---|
| VLAN Segmentation | All devices isolated by role into separate VLANs |
| Firewall Rules | pfSense enforces inter-VLAN routing rules |
| IoT Isolation | IoT / Lab VLAN has no access to any other segment |
| Management Access | Management VLAN restricted to admin accounts only |
| DNS Filtering | pfSense forwards DNS through Cloudflare 1.1.1.1 |

---

## Active Directory Security

| Control | Implementation |
|---|---|
| Least Privilege | Users have standard accounts only |
| Separate Admin Accounts | Admins use dedicated admin accounts for elevated tasks |
| Password Policy | 12 character minimum, complexity required, 90 day expiry |
| Account Lockout | 5 failed attempts triggers 30 minute lockout |
| Admin Group Auditing | Local admin group membership reviewed monthly |
| Disabled Accounts | Inactive accounts disabled after 30 days |

---

## Server Hardening

| Control | Implementation |
|---|---|
| Windows Firewall | Enabled on all Windows VMs, inbound rules locked down |
| RDP Access | Restricted to Management VLAN only |
| SMB Signing | Enabled on all Windows servers |
| Guest Account | Disabled on all machines |
| Auto Updates | Windows Update configured for automatic security patches |
| NTP | All VMs sync time to DC01 |

---

## Access Control

| Control | Implementation |
|---|---|
| MFA | Enabled on all cloud and remote access accounts |
| SSH Keys | Key-based authentication only on Linux VMs, password auth disabled |
| Local Admin | Default local admin account renamed and passworded |
| Service Accounts | Dedicated service accounts used for all scheduled tasks |
| Remote Access | No direct RDP exposed to internet, VPN required |

---

## Patching Policy

| Type | Frequency |
|---|---|
| Windows Security Updates | Automatic, weekly |
| Proxmox Host Updates | Manual review monthly |
| pfSense Updates | Manual review monthly |
| Application Updates | Reviewed and applied quarterly |

---

## Audit and Logging

| Control | Implementation |
|---|---|
| Windows Event Logs | Retained for 30 days on each server |
| Failed Login Attempts | Logged and reviewed weekly |
| Admin Activity | All admin actions logged via Windows Security auditing |
| Firewall Logs | pfSense logs all denied traffic |
| Monitoring Alerts | Grafana alerts on host down and resource thresholds |

---

## Future Improvements

- Deploy a SIEM (Wazuh or Elastic) for centralized log aggregation
- Implement CIS Benchmark hardening on all Windows servers
- Add vulnerability scanning with OpenVAS
- Configure pfSense IDS/IPS using Suricata