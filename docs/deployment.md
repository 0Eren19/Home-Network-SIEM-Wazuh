# Deployment Guide

## Overview

The Home Network SIEM environment was deployed as an isolated virtual laboratory using Oracle VirtualBox.

Four virtual machines were used:

- **pfSense Firewall**
- **Wazuh Server**
- **Windows 10 Endpoint**
- **Kali Linux**

The virtual machines communicate through a VirtualBox Internal Network named `intnet`, while pfSense provides Internet connectivity through NAT.

## 1. Virtual Machine Deployment

The following virtual machines were created:

| Virtual Machine | Operating System | Purpose |
|---|---|---|
| pfSense | pfSense CE | Firewall, Router and DHCP Server |
| Wazuh Server | Ubuntu Server 24.04 LTS | SIEM Platform |
| Windows 10 | Windows 10 22H2 | Monitored Endpoint |
| Kali Linux | Kali Linux 2025 | Attack Simulation and Security Testing |

The laboratory was hosted on a Windows 11 system using Oracle VirtualBox.

## 2. Virtual Network Configuration

An isolated VirtualBox Internal Network named `intnet` was created.

### pfSense

pfSense was configured with two network adapters:

- **Adapter 1:** NAT — Internet/WAN connectivity
- **Adapter 2:** Internal Network (`intnet`) — Laboratory LAN

### Other Virtual Machines

The Wazuh Server, Windows 10 endpoint, and Kali Linux machines were connected to the Internal Network (`intnet`).

This allowed the systems to communicate through pfSense while keeping the laboratory environment isolated from the host network.

## 3. Wazuh Server Deployment

The Wazuh Server was deployed on Ubuntu Server.

The server was configured with the following Wazuh components:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

The services were started and verified after deployment.

### Wazuh Services

| Service | Port | Function |
|---|---:|---|
| Wazuh Manager | 1514, 1515 | Receives logs and manages Wazuh agents |
| Wazuh Dashboard | 443 | Web interface for security monitoring |
| Wazuh Indexer | 9200 | Stores and indexes security events |

## 4. Windows 10 Endpoint Deployment

The Windows 10 virtual machine was configured as the monitored endpoint.

The following components were installed:

- Wazuh Agent 4.14.3
- Microsoft Sysmon

The Wazuh Agent was enrolled with the Wazuh Server and configured to collect Windows security and system events.

Sysmon was used to provide enhanced Windows event logging.

## 5. Log Collection

The Wazuh Agent collected endpoint security telemetry and forwarded it to the Wazuh Server.

Sources included:

- Windows Application events
- Windows Security events
- Windows System events
- Sysmon operational events
- File Integrity Monitoring events

The Wazuh Manager processed the incoming events and applied detection rules.

## 6. Kali Linux Deployment

Kali Linux was configured as the security testing and attack simulation machine.

It was connected to the same Internal Network (`intnet`) as the monitored endpoint and Wazuh Server.

Kali Linux was used to perform controlled testing activities, including:

- Network scanning
- Failed login attempts
- File modification activities
- User account monitoring tests

## 7. Detection and Monitoring Workflow

The deployed environment follows this workflow:

```text
                    Attack / User Activity
                            |
                            v
                     Windows 10 Endpoint
                            |
                   Wazuh Agent + Sysmon
                            |
                            v
                      Wazuh Manager
                            |
                     Event Analysis
                            |
                            v
                      Wazuh Indexer
                            |
                     Event Storage
                            |
                            v
                     Wazuh Dashboard
                            |
                            v
                  Security Monitoring
```

## 8. Deployment Verification

After deployment, the Wazuh services were verified and the Windows endpoint was successfully enrolled.

Once the agent registration and network communication were established, the Windows endpoint began forwarding logs to the Wazuh Server.

Controlled security testing was then performed from Kali Linux and through Windows endpoint activities.

The generated events were detected, analyzed, and displayed through the Wazuh Dashboard.

## 9. Troubleshooting During Deployment

Several deployment issues were encountered during implementation, including:

- Wazuh Indexer failures
- Wazuh Agent connectivity problems
- Network communication errors

These issues were resolved by:

- Verifying service status
- Checking network configuration
- Correcting network settings
- Restarting required services
- Verifying agent registration and communication

## 10. Deployment Outcome

The deployment successfully established an isolated home-network SOC laboratory.

The environment enabled:

- Centralized log collection
- Endpoint monitoring
- Security event analysis
- Network scanning detection
- Authentication failure detection
- File Integrity Monitoring
- User account monitoring
- Threat hunting

The completed environment provided a practical platform for testing Wazuh-based security monitoring and detection capabilities.
