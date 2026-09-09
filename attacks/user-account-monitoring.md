# User Account Monitoring

## Objective

Test whether Wazuh detects Windows user account creation and deletion activities on the monitored Windows 10 endpoint.

## Attack / Test

Windows user account creation and deletion activities were performed on the Windows 10 endpoint as part of the controlled security testing.

The purpose of the test was to validate Wazuh's ability to monitor changes to local user accounts.

## Detection

Wazuh successfully detected the user account changes and generated corresponding security alerts.

The detected events were displayed in the Wazuh Dashboard for analysis.

## Security Relevance

Unauthorized user account changes can indicate:

- Persistence activity
- Unauthorized access
- Privilege escalation attempts
- Account manipulation
- Potential compromise of an endpoint

Monitoring user account changes helps security analysts identify suspicious account-management activity and investigate potential unauthorized access.

## Evidence

### Windows User Account Creation

<img width="960" height="1032" alt="5 13 1 User Account Created Command png" src="https://github.com/user-attachments/assets/227674fd-13a8-40cb-9b48-0ccb688a545e" />

### Wazuh Alert for User Account Creation

<img width="960" height="1032" alt="5 13 2 User Account Event Detected png" src="https://github.com/user-attachments/assets/f4d1a9f1-261f-4ccc-8863-c02c06024595" />


### Windows User Account Deletion

<img width="960" height="1032" alt="5 13 5 User Account Deleted Command png" src="https://github.com/user-attachments/assets/a20c2d89-6923-4a4e-9abc-66df5b6bc6a3" />

### Wazuh Alert for User Account Deletion

<img width="960" height="1032" alt="5 13 6 User Account Deleted Event png" src="https://github.com/user-attachments/assets/a3fb12ab-e28f-4384-9e93-4d780c4d4c3c" />

## Result

**Status: Detected successfully**

The Windows user account creation and deletion activities were detected by Wazuh and the resulting security events were available for analysis in the Wazuh Dashboard.
