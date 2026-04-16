# Network Inventory

## Purpose
This document tracks the active systems and network roles involved in Blue Lab Phase 1. It is intended to provide a clear reference for deployment, troubleshooting, and future expansion while keeping public-facing documentation focused on the lab itself.

## Active Lab Systems

| Device Name | Role | Environment | OS / Platform | IP Address | Notes |
|---|---|---|---|---|---|
| Host Internal NAT Adapter | Internal Lab Gateway | Lab | Hyper-V vEthernet | 10.10.10.1 | Gateway for Blue Lab NAT network |
| Monitoring Server | Lab Server | Lab | Ubuntu Server | 10.10.10.10 | Wazuh manager host |
| Windows Endpoint 1 | Endpoint VM | Lab | Windows 11 | 10.10.10.20 | Active monitored Windows endpoint for Wazuh agent enrollment and event generation |
| Linux Endpoint 1 | Endpoint VM | Lab | Ubuntu Desktop 24.04.4 | 10.10.10.30 | Active monitored Linux endpoint for Wazuh agent enrollment and log collection |
| Kali VM | Supplemental Lab VM | Separate | Kali Linux 2026.1 (VirtualBox) | TBD | Separate VirtualBox VM used for supplemental learning and testing; not part of the primary Hyper-V Phase 1 architecture |

## Environment Notes
- The active lab design uses an Internal Hyper-V switch with NAT.
- The lab subnet is `10.10.10.0/24` and is intentionally separate from the host’s primary network.
- Guest systems use static IP configuration because the Internal NAT design does not provide DHCP.
- The host-side NAT gateway may not respond to ICMP echo from guest systems even when outbound connectivity and DNS resolution are functioning normally.
- A separate Kali Linux VM exists in VirtualBox outside the main Hyper-V Phase 1 build.

## Active Network Summary
- Internal Switch: `BlueLab-Internal`
- NAT Object: `BlueLab-NAT`
- Gateway: `10.10.10.1`
- Wazuh Server: `10.10.10.10`
- Windows Endpoint: `10.10.10.20`
- Linux Endpoint: `10.10.10.30`

## Questions / Unknowns
- What logging enhancements should be added to the Windows endpoint after base OS setup?
- What endpoint telemetry improvements should be added before building the red-lab extension?
- Should the Kali VM eventually be documented in a separate supplemental-lab section rather than the core Phase 1 docs?
- How should the red-lab be segmented on top of the current blue-lab baseline?

## Lab Host Specifications

| Field | Value |
|---|---|
| Host Device Name | `lab-host` |
| Host Operating System | Windows 11 Pro |
| CPU Model | Redacted desktop CPU |
| Number of CPU Cores / Threads | Redacted |
| RAM | 32 GB DDR5 |
| Available Storage for Lab | Tracked separately as needed |
| Virtualization Support Enabled in BIOS | Yes |
| Preferred Virtualization Platform | Hyper-V |

## Notes
- The lab host is used to run the Phase 1 virtual machines.
- Resource allocation remains conservative because host storage and memory must be shared across multiple VMs.
- Hyper-V was enabled successfully and verified after host restart.

## Public Documentation Note
- This inventory intentionally focuses on lab infrastructure rather than documenting the broader home network.
- Non-essential home-environment details are omitted from the public-facing version of this file.
