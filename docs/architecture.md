# Architecture

## Phase 1 Overview
Blue Lab Phase 1 will be a fully virtualized security monitoring lab hosted on a Windows 11 Pro machine using Hyper-V.

The initial environment will include:
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
- Planned OS: Ubuntu Server
- Role: Central monitoring platform
- Purpose: Receive logs and security telemetry from monitored endpoints

### 3. Windows Endpoint
- Planned OS: Windows
- Role: Monitored endpoint
- Purpose: Generate Windows event logs and endpoint activity for monitoring

### 4. Linux Endpoint
- Planned OS: Linux
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
