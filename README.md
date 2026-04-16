# Blue Lab

Blue Lab is a hands-on cybersecurity monitoring lab built to strengthen practical skills in security operations, log analysis, endpoint monitoring, alert validation, and technical documentation.

The project is designed as a portfolio-ready blue-team environment that emphasizes:
- Windows and Linux endpoint monitoring
- Wazuh deployment and agent enrollment
- Hyper-V lab architecture and network troubleshooting
- structured documentation and troubleshooting records
- building a defensive baseline for a future red-lab extension

## Project Purpose

Blue Lab exists to bridge the gap between coursework and real-world security operations practice. The goal is to build, document, and maintain a small but realistic monitoring environment that demonstrates technical growth, disciplined troubleshooting, and clear security-focused documentation.

## Current Phase 1 Environment

Blue Lab Phase 1 is a fully virtualized lab hosted on a Windows 11 Pro machine using Hyper-V.

### Active Systems
- `wazuh-server` — Ubuntu Server 24.04.4 LTS
- `win-endpoint-01` — Windows 11
- `linux-endpoint-01` — Ubuntu Desktop 24.04.4

### Active Network Design
- Hyper-V Internal Switch: `BlueLab-Internal`
- NAT Object: `BlueLab-NAT`
- Lab Subnet: `10.10.10.0/24`

### Static IP Plan
- Gateway: `10.10.10.1`
- Wazuh Server: `10.10.10.10`
- Windows Endpoint: `10.10.10.20`
- Linux Endpoint: `10.10.10.30`

## Current Monitoring Stack

The current deployed monitoring platform for Phase 1 is **Wazuh**.

### Current Status
- Wazuh manager is installed on `wazuh-server`
- Windows agent is installed and enrolled
- Linux agent is installed and enrolled
- Phase 1 currently uses the Wazuh manager component as the deployed baseline

### Notes
- Dashboard and indexer components are not part of the current deployed baseline
- The current build is sufficient for endpoint enrollment, telemetry collection validation, and future detection development

## Phase 1 Goals
- Stand up a functioning monitoring environment
- Connect Windows and Linux endpoints to a central monitoring server
- Confirm endpoint telemetry is being collected
- prepare the environment for basic detections and alert review
- maintain clean, professional documentation from the start

## Project Scope

### In Scope Right Now
- lab planning and documentation
- Hyper-V virtualization
- one Ubuntu monitoring server
- one Windows monitored endpoint
- one Linux monitored endpoint
- centralized log and agent-based monitoring

### Out of Scope Right Now
- cloud integrations
- threat intelligence feeds
- SOAR or case management tools
- advanced DFIR tooling
- complex network segmentation
- public exposure of sensitive environment details

## Repository Focus

This repository is intended to document:
- architecture decisions
- build notes
- installation steps
- troubleshooting history
- tool-selection rationale
- future lab expansion planning

The emphasis is on understanding, repeatability, and clear documentation rather than rushing to add more tools.

## Supplemental Infrastructure

A separate Kali Linux virtual machine exists in VirtualBox for supplemental learning and testing.

### Notes
- it is not part of the primary Blue Lab Phase 1 architecture
- it may later support controlled offensive testing or future red-lab planning

## Public Documentation Note

This repository is sanitized for portfolio use. Public-facing documentation avoids unnecessary exposure of sensitive local environment details, secrets, internal identifiers, and non-essential home-network context.

## Long-Term Direction

Blue Lab Phase 1 serves as the defensive baseline for a future red-lab extension. The long-term plan is to expand from a stable monitored environment into controlled attack simulation, detection validation, and blue-team investigation workflows.
