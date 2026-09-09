# Sysmon Configuration Reference

## Purpose

Sysmon (System Monitor) was installed on the Windows 10 endpoint to provide enhanced Windows event logging for security monitoring.

The Sysmon events were collected by the Wazuh Agent and forwarded to the Wazuh Server for analysis.

## Environment

- Operating System: Windows 10 22H2
- Wazuh Agent: 4.14.3
- Sysmon: Installed on the Windows 10 endpoint
- SIEM: Wazuh

## Sysmon Event Collection

The Wazuh Agent was configured to collect events from the Sysmon operational event channel:

```text
Microsoft-Windows-Sysmon/Operational
```

These events provide additional endpoint telemetry that can support security monitoring and threat detection.

## Security Monitoring

Sysmon telemetry can provide visibility into endpoint activity such as:

- Process activity
- Network-related events
- File activity
- System changes
- Other Windows security-relevant events

The collected telemetry can be analyzed through the Wazuh Dashboard together with Windows Event Logs and other security events.

## Project Usage

In this project, Sysmon was used as an additional source of Windows endpoint telemetry.

The Wazuh Agent collected Sysmon events and forwarded them to the Wazuh Server, where the events could be analyzed and correlated with security monitoring activity.

## Configuration Note

The exact Sysmon XML configuration used during the original deployment is not included in the project report.

Therefore, this file documents the role and integration of Sysmon rather than representing the exact deployed Sysmon configuration.

## Result

**Status: Successfully integrated**

Sysmon provided enhanced Windows event telemetry to support Wazuh-based endpoint monitoring.
