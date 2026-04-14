# Backup Strategy

## Overview
All critical VMs are backed up daily using Veeam Community Edition.
Backups are stored locally on the Proxmox host's secondary HDD and verified
automatically after each job.

---

## Backup Policy

| VM | Frequency | Retention | Type |
|---|---|---|---|
| DC01 | Daily | 7 daily, 4 weekly | Full + Incremental |
| FS01 | Daily | 7 daily, 4 weekly | Full + Incremental |
| MON01 | Weekly | 4 weekly | Full |
| BACKUP01 | Weekly | 4 weekly | Full |

---

## Retention Policy

- **Daily backups:** Kept for 7 days
- **Weekly backups:** Kept for 4 weeks
- **Monthly backups:** Kept for 3 months
- Oldest backups are automatically pruned by Veeam

---

## Backup Window

- Daily jobs run at **11:00 PM** to avoid business hours
- Weekly full backups run **Sunday at 10:00 PM**
- Jobs are expected to complete within 2 hours

---

## Verification

- Veeam SureBackup runs weekly to verify recoverability
- Backup logs are reviewed every Monday morning
- Any failed jobs trigger an email alert to the admin account

---

## Recovery Objectives

| Metric | Target |
|---|---|
| RPO (Recovery Point Objective) | 24 hours |
| RTO (Recovery Time Objective) | 2 hours |

---

## Backup Storage Layout

    BACKUP01 (10.0.20.13)
        |
        |--- D:\Backups\
                |--- DC01\
                |--- FS01\
                |--- MON01\
                |--- BACKUP01\

---

## Offsite / Cloud Consideration

- Current setup is local only
- Future plan: replicate to Backblaze B2 using Veeam Cloud Connect
- Offsite replication would reduce RPO to near zero for critical VMs

---

## Restore Procedure

1. Open Veeam Backup & Replication console
2. Navigate to Home > Backups
3. Right-click the VM > Restore > Entire VM
4. Select restore point and target datastore
5. Power on restored VM and verify functionality
6. Document the restore in the incident log