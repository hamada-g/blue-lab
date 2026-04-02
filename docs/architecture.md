# Architecture

## Phase 1 Overview
Blue Lab Phase 1 is a fully virtualized security monitoring lab hosted on a Windows 11 Pro machine using Hyper-V.

The initial environment includes:
- 1 Ubuntu Server virtual machine for the central monitoring platform
- 1 Windows virtual machine to act as a monitored endpoint
- 1 Linux virtual machine to act as a monitored endpoint

## Planned Components

### 1. Lab Host
- Hostname: Mr-Yeet
- Operating System: Windows 11 Pro
- Virtualization Platform: Hyper-V
- Role: Runs all Phase 1 virtual machines

### 2. Monitoring Server
- Planned OS: Ubuntu Server 24.04 LTS
- Role: Central monitoring platform
- Purpose: Receive logs and security telemetry from monitored endpoints

### 3. Windows Endpoint
- Planned OS: Windows 11
- Role: Monitored endpoint
- Purpose: Generate Windows event logs and endpoint activity for monitoring

### 4. Linux Endpoint
- Planned OS: Ubuntu
- Role: Monitored endpoint
- Purpose: Generate Linux authentication, system, and security-relevant logs

## Phase 1 Data Flow
1. The Windows and Linux endpoints will generate logs and security-relevant activity.
2. The endpoints will forward telemetry to the central monitoring server.
3. The monitoring server will be used to review alerts, logs, and endpoint activity.

## Phase 1 Goals
- Stand up a functioning monitoring environment
- Connect both endpoints to the monitoring server
- Confirm logs are being collected
- Prepare for basic detections and alert review

## Notes
- Phase 1 is intentionally limited in scope.
- Advanced tools such as network sensors, forensic tools, and case management platforms are out of scope for now.
- Public-facing documentation will be sanitized later to remove personal hostnames, IP addresses, and environment-specific details.

## Phase 1 VM Layout

| VM Name | Role | Planned OS | vCPU | RAM | Storage |
|---|---|---|---|---|---|
| wazuh-server | Central monitoring platform | Ubuntu Server | 4 | 8 GB | 50 GB |
| win-endpoint-01 | Monitored Windows endpoint | Windows 11 | 4 | 8 GB | 40 GB |
| linux-endpoint-01 | Monitored Linux endpoint | Ubuntu | 2 | 4 GB | 25 GB |

## Resource Planning Notes
- Phase 1 will use three virtual machines.
- Storage was intentionally reduced to keep the initial lab lightweight and practical.
- Resource assignments may be adjusted later if performance or storage issues arise.

## Phase 1 Network Design Revision
Blue Lab Phase 1 uses an Internal Hyper-V switch with NAT rather than an External switch. This change was made because the External switch bound to the host’s Wi-Fi adapter caused host connectivity instability.

## Revised Network Approach
- The host machine remains connected to the home Wi-Fi network normally.
- The lab virtual machines connect to an Internal Hyper-V switch.
- The host machine provides NAT for the lab network so the virtual machines can reach the internet without directly binding to the physical Wi-Fi adapter.

## Planned Lab Subnet
- Lab Network: 10.10.10.0/24

## Static IP Plan
- Host Internal NAT Gateway: 10.10.10.1
- Wazuh Server: 10.10.10.10
- Windows Endpoint: 10.10.10.20
- Linux Endpoint: 10.10.10.30

## Design Notes
- The lab subnet is intentionally separate from the home network.
- The host machine’s existing IP address and reserved port range on 192.168.5.98 must remain unchanged.
- This design reduces the risk of disrupting host connectivity while still allowing the lab VMs to communicate and access the internet.
- Because the Internal NAT design does not provide DHCP automatically, guest IPs are configured manually.
