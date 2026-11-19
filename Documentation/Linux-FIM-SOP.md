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

### Step 4: Restart Wazuh Agent

Restart the Wazuh agent:

```bash
sudo systemctl restart wazuh-agent
```

Verify the service status:

```bash
sudo systemctl status wazuh-agent
```

Expected status: `active (running)`.

### Step 5: Test File Creation

Create a test file:

```bash
echo "Initial FIM Test" | sudo tee /var/tmp/FIM-Lab/test-file.txt
```

### Step 6: Test File Modification

Modify the existing file:

```bash
echo "Modified FIM Test" | sudo tee /var/tmp/FIM-Lab/test-file.txt
```

### Step 7: Test File Deletion

Delete the test file:

```bash
sudo rm /var/tmp/FIM-Lab/test-file.txt
```

## 4. Wazuh Dashboard Verification

1. Open the Wazuh Dashboard.
2. Navigate to **Threat Hunting → Events**.
3. Search for agent `kali-snort` or agent ID `009`.
4. Review the generated FIM alerts.

Expected Wazuh rule IDs:

| Activity | Rule ID |
|---|---:|
| File Added / Created | `554` |
| File Modified | `550` |
| File Deleted | `553` |

## 5. Result

Wazuh successfully monitored the Kali Linux FIM test directory and generated alerts for file creation, modification, and deletion.

## 6. Conclusion

This lab demonstrated how Wazuh File Integrity Monitoring detects file system changes on a Kali Linux endpoint. It provided practical experience with Linux agent configuration, real-time monitoring, and SIEM alert investigation.
