# File Integrity Monitoring (FIM) on Kali Linux Using Wazuh

## 1. Objective
Configure Wazuh File Integrity Monitoring (FIM) on a Kali Linux endpoint to detect file creation, modification, and deletion in a dedicated test directory.

## 2. Lab Environment
- SIEM: Wazuh
- Endpoint: Kali Linux
- Agent Name: `kali-snort`
- Agent ID: `009`
- Monitored Directory: `/var/tmp/FIM-Lab`
- Agent Configuration: `/var/ossec/etc/ossec.conf`

## 3. Create the FIM Test Directory

Create the test directory:

```bash
sudo mkdir -p /var/tmp/FIM-Lab
```

Verify it:

```bash
ls -ld
