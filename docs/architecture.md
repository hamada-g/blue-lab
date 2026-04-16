# Architecture

## Phase 1 Overview
Blue Lab Phase 1 is a fully virtualized security monitoring lab hosted on a Windows 11 Pro machine using Hyper-V.

The initial environment includes:
- 1 Ubuntu Server virtual machine for the central monitoring platform
- 1 Windows virtual machine to act as a monitored endpoint
- 1 Linux virtual machine to act as a monitored endpoint

## Components

### 1. Lab Host
- Hostname: `lab-host`
- Operating System: Windows 11 Pro
- Virtualization Platform: Hyper-V
- Role: Runs all Phase 1 Hyper-V virtual machines

### 2. Monitoring Server
- OS: Ubuntu Server 24.04.4 LTS
- VM Name: `wazuh-server`
- Role: Central monitoring platform
- Purpose: Receive logs and security telemetry from monitored endpoints

### 3. Windows Endpoint
- OS: Windows 11 English International 64-bit
- VM Name: `win-endpoint-01`
- Role: Monitored endpoint
- Purpose: Generate Windows event logs and endpoint activity for monitoring

### 4. Linux Endpoint
- OS: Ubuntu Desktop 24.04.4
- VM Name: `linux-endpoint-01`
- Role: Monitored endpoint
- Purpose: Generate Linux authentication, system, and security-relevant logs

## Additional Non-Phase-1 VM
A separate Kali Linux virtual machine was also created in VirtualBox for supplemental learning and testing. It is not part of the primary Hyper-V Blue Lab Phase 1 architecture.

## Phase 1 Data Flow
1. The Windows and Linux endpoints generate logs and security-relevant activity.
2. The endpoints forward telemetry to the central monitoring server.
3. The monitoring server is used to review alerts, logs, and endpoint activity.

## Phase 1 Goals
- Stand up a functioning monitoring environment
- Connect both endpoints to the monitoring server
- Confirm logs are being collected
- Prepare for basic detections and alert review

## Notes
- Phase 1 is intentionally limited in scope.
- Advanced tools such as network sensors, forensic tools, case management platforms, and cloud integrations are out of scope for now.
- Public-facing documentation has been sanitized to remove host-specific identifiers, internal file paths, and home-network details.

## Phase 1 VM Layout

| VM Name | Role | OS | vCPU | RAM | Storage | Status |
|---|---|---|---|---|---|---|
| wazuh-server | Central monitoring platform | Ubuntu Server 24.04.4 LTS | 4 | 4 GB | 50 GB | Active |
| win-endpoint-01 | Monitored Windows endpoint | Windows 11 English International 64-bit | 4 | 4 GB | 64 GB dynamic VHDX | Active |
| linux-endpoint-01 | Monitored Linux endpoint | Ubuntu Desktop 24.04.4 | 2 | 3 GB | 25 GB dynamic VHDX | Active |

## Static IP Plan
- Internal NAT Gateway: 10.10.10.1
- Wazuh Server: 10.10.10.10
- Windows Endpoint: 10.10.10.20
- Linux Endpoint: 10.10.10.30

## Phase 1 Network Topology
Blue Lab Phase 1 uses a Hyper-V Internal switch with host-provided NAT.

### Current Network Design
- Host Wi-Fi / home network remains separate from the lab subnet
- Hyper-V Internal switch: `BlueLab-Internal`
- Internal gateway: `10.10.10.1`
- Lab subnet: `10.10.10.0/24`

### Active Core Systems
- `wazuh-server` — 10.10.10.10
- `win-endpoint-01` — 10.10.10.20
- `linux-endpoint-01` — 10.10.10.30

### Notes
- Guest systems use static IP configuration because the lab network does not provide DHCP.
- The current Phase 1 architecture is operational with one monitoring server and two enrolled endpoints.
