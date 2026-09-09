# System Architecture

## Overview

The Home Network SIEM project implements an isolated virtualized Security Operations Center (SOC) environment using Oracle VirtualBox, pfSense, Wazuh, Windows 10, and Kali Linux.

The laboratory consists of four primary virtual machines:

- **pfSense** — Firewall, router, and DHCP server
- **Wazuh Server** — Security Information and Event Management (SIEM) platform
- **Windows 10** — Monitored endpoint
- **Kali Linux** — Attack simulation and security testing

The virtual machines communicate through an isolated VirtualBox Internal Network named `intnet`.

## Architecture Components

### pfSense

pfSense acts as the central network gateway and firewall.

Its responsibilities include:

- Network routing
- Firewall and traffic filtering
- DHCP services
- Internet connectivity through NAT

The pfSense virtual machine uses two network interfaces:

- **Adapter 1:** NAT network for Internet/WAN connectivity
- **Adapter 2:** VirtualBox Internal Network (`intnet`) for the laboratory LAN

### Wazuh Server

The Wazuh Server provides the centralized SIEM platform.

The server runs on Ubuntu Server and includes:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

The Wazuh Manager receives and analyzes security events, the Wazuh Indexer stores and indexes the processed events, and the Wazuh Dashboard provides the interface for security monitoring and analysis.

### Windows 10 Endpoint

The Windows 10 virtual machine acts as the monitored endpoint.

The endpoint includes:

- Wazuh Agent
- Microsoft Sysmon
- Windows Event Logs
- Security and system event monitoring

The Wazuh Agent collects endpoint security events and forwards them to the Wazuh Server.

### Kali Linux

Kali Linux is used for controlled security testing and attack simulation.

Testing activities include:

- Network scanning
- Failed login attempts
- File modification activities
- Other controlled security testing

The generated events are monitored through Wazuh.

## Network Topology

```text
                    Internet
                       │
                    NAT / WAN
                       │
                 ┌───────────┐
                 │  pfSense  │
                 │ Firewall  │
                 │  Router   │
                 └─────┬─────┘
                       │
              Internal Network
                   (intnet)
                       │
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Wazuh       │ │ Windows 10  │ │ Kali Linux  │
│ Server      │ │ Endpoint    │ │             │
│             │ │             │ │ Attack /    │
│ Manager     │ │ Wazuh Agent │ │ Security    │
│ Indexer     │ │ Sysmon      │ │ Testing     │
│ Dashboard   │ │             │ │             │
└─────────────┘ └─────────────┘ └─────────────┘
```

## Network Configuration

| Virtual Machine | Network | Purpose |
|---|---|---|
| pfSense | NAT | Internet / WAN |
| pfSense | Internal Network (`intnet`) | LAN / Internal Network |
| Wazuh Server | Internal Network (`intnet`) | SIEM communication |
| Windows 10 | Internal Network (`intnet`) | Endpoint communication |
| Kali Linux | Internal Network (`intnet`) | Attack simulation |

## Security Event Data Flow

The security monitoring process follows this sequence:

```text
User Activity / Attack Simulation
              |
              v
       Windows 10 Endpoint
              |
              v
         Wazuh Agent
              |
              v
        Wazuh Manager
              |
       Detection & Analysis
              |
              v
        Wazuh Indexer
              |
        Storage & Indexing
              |
              v
       Wazuh Dashboard
              |
              v
   Security Monitoring / Analysis
```

### Data Flow Process

1. User activities or controlled attack simulations generate security events on the Windows 10 endpoint.
2. The Wazuh Agent collects security logs and system events.
3. The collected events are forwarded to the Wazuh Manager.
4. The Wazuh Manager analyzes events, applies detection rules, and generates security alerts.
5. Processed events are indexed and stored in the Wazuh Indexer.
6. The Wazuh Dashboard retrieves the indexed data and displays alerts and security information.
7. Security analysis and threat hunting can then be performed using the generated events.

## Implemented Wazuh Services

| Service | Port | Function |
|---|---:|---|
| Wazuh Manager | 1514, 1515 | Receives logs and manages Wazuh agents |
| Wazuh Dashboard | 443 | Web interface for security monitoring |
| Wazuh Indexer | 9200 | Stores and indexes security events |
| Wazuh Agent | 1514, 1515 | Collects and forwards endpoint logs |
| pfSense Firewall | LAN/WAN | Routing, firewall, and network security |

## Architecture Objective

The architecture provides an isolated environment for:

- Centralized security monitoring
- Endpoint log collection
- Network security monitoring
- Attack simulation
- Threat detection
- Threat hunting
- Security event analysis
- Incident investigation

The environment is designed to simulate a small enterprise-style SOC while keeping the laboratory network isolated from the host network.
