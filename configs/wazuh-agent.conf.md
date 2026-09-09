# Wazuh Agent Configuration Reference

```xml
<!--
Wazuh Agent Configuration Reference

Project: Home Network SIEM

Endpoint:
- Windows 10 22H2
- Wazuh Agent 4.14.3
- Sysmon installed for enhanced Windows event logging

Note:
This file documents the configuration areas used in the project.
Values that depend on the local deployment should be adjusted accordingly.
-->

<ossec_config>

  <!-- Wazuh Manager Connection -->
  <client>
    <server>
      <address>WAZUH_SERVER_IP</address>
      <port>1514</port>
      <protocol>tcp</protocol>
    </server>
  </client>

  <!-- Windows Event Logs -->
  <localfile>
    <location>Application</location>
    <log_format>eventchannel</log_format>
  </localfile>

  <localfile>
    <location>Security</location>
    <log_format>eventchannel</log_format>
  </localfile>

  <localfile>
    <location>System</location>
    <log_format>eventchannel</log_format>
  </localfile>

  <!-- Sysmon -->
  <localfile>
    <location>Microsoft-Windows-Sysmon/Operational</location>
    <log_format>eventchannel</log_format>
  </localfile>

</ossec_config>
```
