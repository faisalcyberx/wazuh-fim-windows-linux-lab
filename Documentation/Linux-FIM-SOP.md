# File Integrity Monitoring (FIM) on Kali Linux Using Wazuh

## 1. Objective

Configure Wazuh File Integrity Monitoring (FIM) on a Kali Linux endpoint to detect file creation, modification, and deletion activities in a dedicated test directory.

Verify the generated security alerts through the Wazuh Dashboard.

## 2. Lab Environment

| Component | Details |
|---|---|
| SIEM | Wazuh on AWS EC2 |
| Endpoint | Kali Linux |
| Agent Name | `kali-snort` |
| Agent ID | `009` |
| Monitoring Feature | Wazuh Syscheck |
| Monitored Directory | `/var/tmp/FIM-Lab` |

## 3. Implementation Steps

### Step 1: Verify Wazuh Agent

Check the Wazuh agent service:

```bash
sudo systemctl status wazuh-agent
```

Expected status: `active (running)`.

### Step 2: Create FIM Test Directory

Create the directory:

```bash
sudo mkdir -p /var/tmp/FIM-Lab
```

Verify it:

```bash
ls -ld /var/tmp/FIM-Lab
```

### Step 3: Configure Linux FIM

Open the Wazuh agent configuration file:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add the following entry inside the existing `<syscheck>` section:

```xml
<directories check_all="yes" realtime="yes">/var/tmp/FIM-Lab</directories>
```

Ensure FIM is enabled:

```xml
<disabled>no</disabled>
```

Save the configuration.

### Step 4: Restart Wazuh
