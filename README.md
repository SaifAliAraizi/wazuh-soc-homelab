# Wazuh SOC Home Lab

A hands-on Security Operations Center (SOC) lab built from scratch using **Wazuh** as the SIEM/XDR platform.  
The goal of this project is to simulate a real SOC environment: collect telemetry from endpoints, detect suspicious activity, monitor file integrity, and gradually add threat intelligence, network detection, and automated response.

> This is an ongoing project. Each phase is documented in the `docs/` folder with configuration files and screenshots.

---

## 📌 Current Status

| Phase | Component | Status |
|-------|-----------|--------|
| 1 | Wazuh Server (Manager + Indexer + Dashboard) on Rocky Linux | ✅ Done |
| 2 | Windows 10 Agent deployment | ✅ Done |
| 3 | Sysmon integration (process, network, file telemetry) | ✅ Done |
| 4 | Windows Event Log collection (Security, System, Sysmon Operational) | ✅ Done |
| 5 | File Integrity Monitoring (FIM) with real-time alerts | ✅ Done |
| 6 | Security Configuration Assessment (CIS Benchmark) | ✅ Done (default) |
| 7 | VirusTotal integration | 🔜 Planned |
| 8 | Active Response (automated endpoint response) | 🔜 Planned |
| 9 | Suricata IDS (network-level detection) | 🔜 Planned |
| 10 | EVE-NG network topology integration | 🔜 Planned |

---

## 🏗️ Architecture

![Architecture](architecture/diagram.png)

- **Hypervisor:** VMware Workstation (local laptop)
- **Wazuh Server:** Rocky Linux 9 — Wazuh Manager, Indexer, Dashboard (all-in-one)
- **Endpoint:** Windows 10 Pro — Wazuh Agent + Sysmon
- **Network:** Isolated host-only / NAT lab network

See [docs/01-architecture.md](docs/01-architecture.md) for details.

---

## 📂 Documentation

| # | Document | Description |
|---|----------|-------------|
| 01 | [Architecture](docs/01-architecture.md) | Lab design, VMs, network layout |
| 02 | [Wazuh Installation](docs/02-wazuh-installation.md) | Installing the Wazuh server on Rocky Linux |
| 03 | [Windows Agent + Sysmon](docs/03-windows-agent-sysmon.md) | Deploying the agent and integrating Sysmon |
| 04 | [File Integrity Monitoring](docs/04-fim-configuration.md) | Real-time FIM configuration and testing |
| 05 | [Detections Observed](docs/05-detections-observed.md) | Alerts triggered during testing |
| — | [Roadmap](docs/roadmap.md) | Upcoming integrations |

---

## 📸 Screenshots

| Wazuh Dashboard | Agent Connected |
|---|---|
| ![Dashboard](screenshots/01-dashboard-overview.png) | ![Agents](screenshots/02-agent-active.png) |

| Sysmon Events in Wazuh | FIM Alert |
|---|---|
| ![Sysmon](screenshots/03-sysmon-events.png) | ![FIM](screenshots/04-fim-alert.png) |

---

## 🔍 Sample Detections Achieved So Far

- Suspicious PowerShell execution (`SecEdit.exe` launched from PowerShell)
- PowerShell used to delete files or directories
- Discovery activity (`net.exe` / `net user`) via Sysmon Event ID 1
- Windows command shell started by an abnormal process
- Executable dropped in Windows root folder (FIM)
- File added / deleted in monitored directories (real-time FIM)
- CIS Microsoft Windows 10 Benchmark compliance checks (SCA)

---

## 🛠️ Technologies

`Wazuh 4.x` · `Rocky Linux 9` · `Windows 10 Pro` · `Sysmon` · `OpenSearch (Wazuh Indexer)` · `Filebeat` · `VMware Workstation`

---

## 📁 Repository Structure
