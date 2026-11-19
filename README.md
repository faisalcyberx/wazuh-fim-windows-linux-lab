# File Integrity Monitoring (FIM) on Windows & Linux Using Wazuh

## Project Overview

This project demonstrates File Integrity Monitoring (FIM) using Wazuh on Windows and Kali Linux endpoints.

The lab focuses on detecting file creation, modification, and deletion activities through the Wazuh Dashboard.

## Lab Environment

- **SIEM:** Wazuh
- **Manager:** AWS EC2
- **Windows Endpoint:** Windows
- **Linux Endpoint:** Kali Linux
- **Monitoring Feature:** File Integrity Monitoring (FIM)

## Lab Objectives

- Configure FIM on Windows and Kali Linux.
- Monitor specific directories for file changes.
- Detect file creation, modification, and deletion.
- Verify generated security alerts in Wazuh Dashboard.

## Activities Performed

1. Created dedicated FIM test directories.
2. Configured monitored paths in the Wazuh agent configuration.
3. Restarted the agents after configuration changes.
4. Created test files.
5. Modified existing files.
6. Deleted test files.
7. Verified the generated alerts in Wazuh Dashboard.

## Expected Wazuh Rule IDs

| Activity | Rule ID |
|---|---|
| File Added | 554 |
| File Modified | 550 |
| File Deleted | 553 |

## Results

Wazuh successfully detected file creation, modification, and deletion activities on both Windows and Kali Linux endpoints.

## Skills Demonstrated

- SIEM Monitoring
- Wazuh Agent Configuration
- File Integrity Monitoring
- Windows Security Monitoring
- Linux Security Monitoring
- Security Alert Investigation

## Author

Faisal CyberX

Cybersecurity | SOC Analyst Learning Journey
