# Failed Login Detection

## Objective

Test whether Wazuh detects multiple failed login attempts on the monitored Windows 10 endpoint.

## Attack / Test

Multiple failed login attempts were generated on the Windows 10 endpoint as a controlled security testing activity.

The test was performed to generate authentication failure events for Wazuh monitoring.

## Detection

Wazuh detected the authentication failures and generated a corresponding security alert.

The detected event was also mapped to the appropriate MITRE ATT&CK technique.

## Security Relevance

Repeated failed login attempts can indicate:

- Brute-force activity
- Password guessing
- Unauthorized access attempts
- Account compromise attempts

Monitoring authentication failures helps security analysts identify suspicious login activity and investigate potential attacks.

## Evidence

### Failed Login Detection

<img width="960" height="1032" alt="5 9 1 Failed Windows Login Detection png" src="https://github.com/user-attachments/assets/f035eef9-d97b-430a-8fba-645d281d32b4" />

## Result

**Status: Detected successfully**

The failed login attempts were detected by Wazuh and the resulting security event was analyzed through the Wazuh Dashboard.
