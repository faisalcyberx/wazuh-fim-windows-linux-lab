# Linux File Integrity Monitoring (FIM) Using Wazuh

## 1. Objective

Configure Wazuh File Integrity Monitoring (FIM) on a Kali Linux endpoint to detect:

- File creation
- File modification
- File deletion

Verify the generated security alerts in the Wazuh Dashboard.

## 2. Lab Environment

| Component | Details |
|---|---|
| SIEM | Wazuh on AWS EC2 |
| Linux Agent | kali-snort (009) |
| Operating System | Kali Linux |
| Monitoring Feature | Wazuh Syscheck |
| FIM Test Directory | `/var/tmp/FIM-Lab` |

## 3. Implementation Steps

### Step 8: Verify Linux Agent

Open the Kali Linux terminal and execute:

```bash
sudo systemctl status wazuh-agent
```

Expected status: `Active (running)`.

**Screenshot 08:** `08-linux-agent-status.png`

### Step 9: Create Test Directory

Execute:

```bash
sudo mkdir -p /var/tmp/FIM
