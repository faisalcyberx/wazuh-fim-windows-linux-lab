# Windows File Integrity Monitoring (FIM) Using Wazuh

## 1. Objective

Configure Wazuh File Integrity Monitoring (FIM) on a Windows 10 endpoint to detect:

- File creation
- File modification
- File deletion

Verify the generated security alerts in the Wazuh Dashboard.

## 2. Lab Environment

| Component | Details |
|---|---|
| SIEM | Wazuh on AWS EC2 |
| Windows Agent | windows-agent-03 (005) |
| Operating System | Windows 10 |
| Monitoring Feature | Wazuh Syscheck |
| FIM Test Directory | `C:\FIM-Lab` |

## 3. Implementation Steps

### Step 1: Verify Windows Agent

Open PowerShell as Administrator and execute:

```powershell
Get-Service WazuhSvc
```

Expected status: `Running`

**Screenshot 01:** `01-windows-agent-status.png`

### Step 2: Create Test Directory

Execute:

```powershell
New-Item -ItemType Directory -Path "C:\FIM-Lab" -Force
```

This directory will be monitored by the Wazuh Agent.

**Screenshot 02:** `02-windows-fim-directory.png`

### Step 3: Configure Windows FIM

Open the Wazuh Agent configuration file:

`C:\Program Files (x86)\ossec-agent\ossec.conf`

Add the following entry inside the existing `<syscheck>` section:

```xml
<directories check_all="yes" realtime="yes">C:\FIM-Lab</directories>
```

Ensure FIM is enabled:

```xml
<disabled>no</disabled>
```

Save the configuration.

The Wazuh Windows Agent monitors the specified directory based on the configuration defined in the `syscheck` section of `ossec.conf`.

**Screenshot 03:** `03-windows-fim-config.png`

### Step 4: Restart Windows Agent

Open PowerShell as Administrator and execute:

```powershell
Restart-Service WazuhSvc
Get-Service WazuhSvc
```

Expected status: `Running`

**Screenshot 04:** `04-windows-agent-restarted.png`

### Step 5: Test File Creation

Create a test file:

```powershell
"Initial FIM Test" | Out-File C:\FIM-Lab\test-file.txt
```

**Screenshot 05:** `05-windows-file-creation.png`

### Step 6: Test File Modification

Modify the existing file:

```powershell
"Modified FIM Test" | Out-File C:\FIM-Lab\test-file.txt
```

**Screenshot 06:** `06-windows-file-modification.png`

### Step 7: Test File Deletion

Delete the test file:

```powershell
Remove-Item C:\FIM-Lab\test-file.txt
```

**Screenshot 07:** `07-windows-file-deletion.png`

## 4. Result

Wazuh successfully monitored the Windows FIM test directory and generated alerts for file creation, modification, and deletion.

## 5. Conclusion

This practical exercise demonstrated how Wazuh FIM monitors file system changes on a Windows endpoint. It also provided hands-on experience with agent configuration, file monitoring, and security alert verification.
