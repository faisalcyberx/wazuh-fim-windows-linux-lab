# File Integrity Monitoring (FIM) on Windows & Linux Using Wazuh

## Project Overview

This hands-on cybersecurity lab demonstrates **File Integrity Monitoring (FIM)** using Wazuh across Windows 10 and Kali Linux endpoints.

The project focuses on monitoring designated directories and detecting file creation, modification, and deletion events. Generated security alerts were investigated and verified through the Wazuh Dashboard.

## Lab Architecture

| Component | Details |
|---|---|
| SIEM Platform | Wazuh |
| Wazuh Manager | AWS EC2 |
| Windows Endpoint | Windows 10 |
| Windows Agent | `windows-agent-03 (005)` |
| Linux Endpoint | Kali Linux |
| Linux Agent | `kali-snort (009)` |
| Monitoring Feature | File Integrity Monitoring (FIM) |

## Monitored Directories

| Endpoint | Monitored Directory |
|---|---|
| Windows 10 | `C:\FIM-Lab` |
| Kali Linux | `/var/tmp/FIM-Lab` |

## Lab Objectives

- Configure File Integrity Monitoring on Windows and Kali Linux.
- Monitor dedicated directories for file system changes.
- Detect file creation, modification, and deletion activities.
- Generate and investigate Wazuh security alerts.
- Validate endpoint monitoring through the Wazuh Dashboard.

## Implementation

1. Created dedicated FIM test directories on both endpoints.
2. Configured monitored directories in the existing Wazuh agent configuration files.
3. Enabled real-time monitoring.
4. Restarted Wazuh agents to apply configuration changes.
5. Created test files in monitored directories.
6. Modified existing test files.
7. Deleted test files.
8. Investigated the generated events in Wazuh Dashboard under **Threat Hunting → Events**.

## Configuration Files

The following configuration examples contain the relevant FIM configuration snippets:

- [Windows FIM Configuration](Configuration/windows-fim-config.xml)
- [Linux FIM Configuration](Configuration/linux-fim-config.xml)

**Actual agent configuration file locations:**

- Windows: `C:\Program Files (x86)\ossec-agent\ossec.conf`
- Kali Linux: `/var/ossec/etc/ossec.conf`

## Detection Results

Wazuh successfully generated alerts for file system activities on both endpoints.

| Activity | Wazuh Rule ID |
|---|---:|
| File Added / Created | `554` |
| File Modified | `550` |
| File Deleted | `
