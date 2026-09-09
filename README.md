# 🛡️ Home Network SIEM – Wazuh

> A virtualized Security Operations Center (SOC) environment for security monitoring, endpoint detection, log analysis, threat detection, and controlled attack simulation.

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-blue)](https://wazuh.com/)
[![pfSense](https://img.shields.io/badge/Firewall-pfSense-orange)](https://www.pfsense.org/)
[![Windows](https://img.shields.io/badge/Endpoint-Windows%2010-blue)](https://www.microsoft.com/windows)
[![Kali Linux](https://img.shields.io/badge/Security-Kali%20Linux-557C94)](https://www.kali.org/)
[![VirtualBox](https://img.shields.io/badge/Virtualization-VirtualBox-183A61)](https://www.virtualbox.org/)

---

## 🎯 Project Overview

This project implements an isolated home-network Security Operations Center (SOC) environment using Oracle VirtualBox, pfSense, Wazuh, Windows 10, and Kali Linux.

The environment is designed to demonstrate practical cybersecurity concepts including:

- Centralized security monitoring
- SIEM deployment
- Endpoint log collection
- Security event analysis
- Threat detection
- File Integrity Monitoring (FIM)
- Authentication monitoring
- User account monitoring
- Network reconnaissance detection
- Controlled attack simulation
- Threat hunting
- Security investigation

The laboratory consists of four primary virtual machines.

| Component | Role |
|---|---|
| 🛡️ pfSense | Firewall, router, DHCP server, and network gateway |
| 🔎 Wazuh Server | Centralized SIEM and security monitoring |
| 💻 Windows 10 | Monitored endpoint |
| 🐉 Kali Linux | Security testing and attack simulation |

The virtual machines communicate through an isolated VirtualBox Internal Network named `intnet`.

---

## 🚨 Detection Results

The environment was validated using controlled security testing activities.

| Security Test | Purpose | Result |
|---|---|---|
| 🔍 Nmap Network Scan | Network reconnaissance detection | ✅ Detected |
| 🔐 Failed Login Attempts | Authentication monitoring | ✅ Detected |
| 📁 File Modification | File Integrity Monitoring | ✅ Detected |
| 👤 User Account Creation | Account activity monitoring | ✅ Detected |
| 👤 User Account Deletion | Account activity monitoring | ✅ Detected |

### Validation Result

**5/5 implemented detection scenarios successfully detected.**

The detected events were analyzed through the Wazuh Dashboard.

---

## 🏗️ Architecture

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

### Architecture Components

#### 🛡️ pfSense

pfSense acts as the central network gateway and firewall.

Responsibilities include:

- Network routing
- Firewall and traffic filtering
- DHCP services
- Internet connectivity through NAT

The pfSense virtual machine uses:

- **Adapter 1:** NAT network for Internet/WAN connectivity
- **Adapter 2:** VirtualBox Internal Network (`intnet`) for the laboratory LAN

#### 🔎 Wazuh Server

The Wazuh Server provides the centralized SIEM platform.

The server runs on Ubuntu Server and includes:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

The Wazuh Manager receives and analyzes security events, the Wazuh Indexer stores and indexes processed events, and the Wazuh Dashboard provides the interface for security monitoring and analysis.

#### 💻 Windows 10 Endpoint

The Windows 10 virtual machine acts as the monitored endpoint.

The endpoint includes:

- Wazuh Agent
- Microsoft Sysmon
- Windows Event Logs
- Security and system event monitoring

The Wazuh Agent collects endpoint security events and forwards them to the Wazuh Server.

#### 🐉 Kali Linux

Kali Linux is used for controlled security testing and attack simulation.

Testing activities include:

- Network scanning
- Failed login attempts
- File modification activities
- Other controlled security testing

The generated security events are monitored through Wazuh.

---

## 🔄 Security Event Flow

```text
User Activity / Attack Simulation
              │
              ▼
       Windows 10 Endpoint
              │
              ▼
         Wazuh Agent
              │
              ▼
        Wazuh Manager
              │
       Detection & Analysis
              │
              ▼
        Wazuh Indexer
              │
       Storage & Indexing
              │
              ▼
       Wazuh Dashboard
              │
              ▼
    Security Monitoring
       / Investigation
```

### Data Flow Process

1. User activities or controlled attack simulations generate security events on the Windows 10 endpoint.
2. The Wazuh Agent collects security logs and system events.
3. The collected events are forwarded to the Wazuh Manager.
4. The Wazuh Manager analyzes events, applies detection rules, and generates security alerts.
5. Processed events are indexed and stored in the Wazuh Indexer.
6. The Wazuh Dashboard retrieves the indexed data and displays alerts and security information.
7. Security analysis and threat hunting can then be performed using the generated events.

---

## 🧪 Security Testing

The project uses controlled security testing to validate the monitoring and detection capabilities of the SIEM environment.

### 🔍 Network Reconnaissance Detection

An Nmap operating system detection scan was performed from the Kali Linux virtual machine against the Windows 10 endpoint.

The activity was used to generate network reconnaissance events for Wazuh monitoring.

**Result:** ✅ Detected successfully

See:

[`attacks/nmap-scan.md`](attacks/nmap-scan.md)

---

### 🔐 Failed Login Detection

Multiple failed login attempts were generated on the Windows 10 endpoint.

The purpose was to validate authentication monitoring and generate security events for analysis.

The detected event was also mapped to the appropriate MITRE ATT&CK technique.

**Result:** ✅ Detected successfully

See:

[`attacks/failed-login.md`](attacks/failed-login.md)

---

### 📁 File Integrity Monitoring

A file modification activity was performed on the monitored Windows 10 endpoint.

The test validated Wazuh's File Integrity Monitoring capability.

**Result:** ✅ Detected successfully

See:

[`attacks/file-modification.md`](attacks/file-modification.md)

---

### 👤 User Account Monitoring

Windows user account creation and deletion activities were performed on the Windows 10 endpoint.

The purpose was to validate Wazuh's ability to monitor changes to local user accounts.

**Result:** ✅ Detected successfully

See:

[`attacks/user-account-monitoring.md`](attacks/user-account-monitoring.md)

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| 🛡️ Wazuh | SIEM, security monitoring, detection and alerting |
| 🔥 pfSense | Firewall, routing and DHCP |
| 💻 Windows 10 | Monitored endpoint |
| 🐉 Kali Linux | Security testing and attack simulation |
| 📊 Microsoft Sysmon | Enhanced Windows endpoint telemetry |
| 🖥️ Ubuntu Server | Wazuh Server operating system |
| 📦 Oracle VirtualBox | Virtualization platform |
| 🔎 Nmap | Network reconnaissance testing |
| 🎯 MITRE ATT&CK | Attack technique mapping |

---

## 🖥️ Environment

| Component | Technology |
|---|---|
| Virtualization | Oracle VirtualBox |
| Firewall / Router | pfSense CE |
| SIEM | Wazuh |
| SIEM Server OS | Ubuntu Server |
| Monitored Endpoint | Windows 10 22H2 |
| Endpoint Agent | Wazuh Agent 4.14.3 |
| Endpoint Telemetry | Microsoft Sysmon |
| Security Testing | Kali Linux |
| Network | VirtualBox Internal Network (`intnet`) |

---

## 📂 Repository Structure

```text
Home-Network-SIEM-Wazuh/
│
├── attacks/
│   ├── nmap-scan.md
│   ├── failed-login.md
│   ├── file-modification.md
│   └── user-account-monitoring.md
│
├── configs/
│   ├── wazuh-agent.conf
│   ├── ossec-reference.md
│   └── sysmon-config-reference.md
│
├── docs/
│   ├── architecture.md
│   ├── deployment.md
│   ├── detection-methodology.md
│   └── Home-Network-SIEM-Project-Report.pdf
│
├── images/
│
├── screenshots/
│
├── scripts/
│
├── .gitignore
├── LICENSE
└── README.md
```

---

## 📚 Documentation

| Document | Description |
|---|---|
| [🏗️ Architecture](docs/architecture.md) | System architecture, network topology and security event flow |
| [🚀 Deployment](docs/deployment.md) | Virtual machine and SIEM deployment process |
| [🔬 Detection Methodology](docs/detection-methodology.md) | Security testing and detection methodology |
| [🧪 Attack Tests](attacks/) | Individual security testing scenarios |
| [⚙️ Configuration References](configs/) | Wazuh Agent, Wazuh Manager and Sysmon references |
| [📄 Project Report](docs/Home-Network-SIEM-Project-Report.pdf) | Complete project report |

---

## 🔐 Key Security Concepts Demonstrated

### SIEM

Centralized collection, analysis, indexing, and visualization of security events using Wazuh.

### Endpoint Monitoring

Windows security and system events are collected through the Wazuh Agent.

### Sysmon Telemetry

Microsoft Sysmon provides additional Windows endpoint telemetry to support security monitoring and investigation.

### File Integrity Monitoring

Wazuh monitors configured files and generates security events when monitored files are modified.

### Authentication Monitoring

Failed login attempts are monitored to identify suspicious authentication activity.

### Account Monitoring

Windows user account creation and deletion events are monitored for potential unauthorized account manipulation.

### Network Reconnaissance Detection

Controlled Nmap scanning from Kali Linux is used to validate detection of network reconnaissance activity.

### MITRE ATT&CK

Detected security events can be mapped to relevant MITRE ATT&CK techniques to provide additional context during investigation.

---

## 📊 Implemented Wazuh Services

| Service | Port | Function |
|---|---|---|
| Wazuh Manager | 1514, 1515 | Receives logs and manages Wazuh agents |
| Wazuh Dashboard | 443 | Web interface for security monitoring |
| Wazuh Indexer | 9200 | Stores and indexes security events |
| Wazuh Agent | 1514, 1515 | Collects and forwards endpoint logs |
| pfSense Firewall | LAN/WAN | Routing, firewall and network security |

---

## 🎯 Project Objectives

The project was designed to build a practical and isolated SOC-style environment for learning and demonstrating:

- SIEM deployment
- Security monitoring
- Endpoint telemetry
- Log collection
- Threat detection
- File Integrity Monitoring
- Network reconnaissance detection
- Authentication monitoring
- Account activity monitoring
- Threat hunting
- Security investigation
- Attack simulation

---

## 📈 Project Outcome

The completed environment demonstrates how a small SOC-style architecture can be built using virtualization and open-source security technologies.

The project successfully demonstrates the collection, detection, analysis, and investigation of security events generated during controlled testing.

### Detection Validation

**5/5 implemented detection scenarios successfully detected.**

The project provides practical exposure to:

- SIEM operations
- Endpoint security monitoring
- Security event analysis
- Network security
- Detection engineering concepts
- Incident investigation
- MITRE ATT&CK analysis

---

## ⚠️ Disclaimer

All security testing performed in this project was conducted in an isolated and controlled laboratory environment for educational and defensive security purposes.

The techniques and tools documented in this repository should only be used on systems and networks where you have explicit authorization to perform security testing.

---

## 👤 Author

**Mohammad Arshad**

Cybersecurity Student | Security Operations | SIEM | Defensive Security
