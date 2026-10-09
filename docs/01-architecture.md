# 01 - Lab Architecture

## Overview

The lab runs on a single laptop using VMware Workstation. A Wazuh all-in-one server on Rocky Linux collects and analyzes telemetry from a Windows 10 endpoint.

## Components

| Role | OS | Software | Notes |
|---|---|---|---|
| SIEM / XDR server | Rocky Linux [VERSION] | Wazuh Manager, Indexer, Filebeat, Dashboard | All-in-one install, [X] vCPU / [X] GB RAM |
| Monitored endpoint | Windows 10 Pro (build 19045) | Wazuh Agent 4.14.x, Sysmon | Agent name: `win-10` |
| Hypervisor | Host laptop | VMware Workstation [VERSION] | [Network mode: NAT / Host-only / Bridged] |

## Network Layout

| Host | IP | Role |
|---|---|---|
| Wazuh server | `<MANAGER_IP>` | Manager + Dashboard |
| win-10 | `<AGENT_IP>` | Monitored endpoint |

Subnet: `[x.x.x.0/24]`, VMware [mode].

## Data Flow

```text
Windows Event Log (Sysmon/Operational, Security, System)
        │
        ▼
Wazuh Agent ──(1514/tcp, encrypted)──► Wazuh Manager
                                         │  decoders + rules + MITRE mapping
                                         ▼
                                    Filebeat ──► Wazuh Indexer ──► Dashboard (Discover, MITRE, FIM, SCA)
```

FIM (syscheck) and Security Configuration Assessment (SCA) run inside the same agent and report through the same channel.

## Ports Used

| Port | Protocol | Purpose |
|---|---|---|
| 1514 | TCP | Agent → Manager event communication |
| 1515 | TCP | Agent enrollment |
| 55000 | TCP | Wazuh server API |
| 443 | TCP | Wazuh Dashboard (HTTPS) |
| 9200 | TCP | Wazuh Indexer (internal) |

## Architecture Diagram

![Architecture diagram](../screenshots/architecture-diagram.png)

*(Create with draw.io or Excalidraw and export as PNG.)*

## Planned Extensions

- **Suricata** on a network sensor feeding `eve.json` to Wazuh
- **EVE-NG** for a larger simulated network with multiple devices
- **VirusTotal** integration for hash enrichment on FIM events
- **Active Response** to automatically block or remove malicious indicators

See [ROADMAP](../ROADMAP.md).