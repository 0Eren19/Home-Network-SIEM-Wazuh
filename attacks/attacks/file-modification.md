# File Integrity Monitoring Detection

## Objective

Test whether Wazuh detects unauthorized or suspicious modifications to monitored files on the Windows 10 endpoint.

## Attack / Test

A file modification activity was performed on the monitored Windows 10 endpoint as part of the controlled security testing.

The test was conducted to validate Wazuh's File Integrity Monitoring (FIM) capability.

## Detection

Wazuh monitored the configured files and detected the file modification event.

The resulting security event was displayed in the Wazuh Dashboard for analysis.

## Security Relevance

Unexpected file modifications can indicate:

- Unauthorized changes
- Malware activity
- Persistence mechanisms
- Tampering with system or application files
- Potential compromise of an endpoint

File Integrity Monitoring helps security analysts identify changes to important files and investigate potentially suspicious activity.

## Evidence

### File Modification Detection

<img width="960" height="1032" alt="image" src="https://github.com/user-attachments/assets/3a810fd6-c93f-431c-ba36-ec0a86005c2d" />

## Result

**Status: Detected successfully**

The file modification activity was detected by Wazuh through File Integrity Monitoring and the resulting event was available for analysis in the Wazuh Dashboard.
