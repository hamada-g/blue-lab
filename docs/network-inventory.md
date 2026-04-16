# Network Inventory

## Purpose
This document tracks the systems, devices, and network roles involved in Blue Lab. It is intended to separate personal/home infrastructure from lab infrastructure and provide a clear reference for future deployment and troubleshooting.

## Device Inventory

| Device Name | Role | Environment | OS / Platform | IP Address | Notes |
|---|---|---|---|---|---|
| Home Router | Router / Gateway | Home | Consumer router | 10.255.255.1 | Sanitized home-network gateway reference |
| Main PC / Laptop | Lab Host | Home | Windows 11 Pro | 10.255.255.10 | Sanitized host-side network reference |
| Host Internal NAT Adapter | Internal Lab Gateway | Lab | Hyper-V vEthernet | 10.10.10.1 | Gateway for Blue Lab NAT network |
| Monitoring Server | Lab Server | Lab | Ubuntu Server | 10.10.10.10 | Wazuh manager host |
| Windows Endpoint 1 | Endpoint VM | Lab | Windows 11 | 10.10.10.20 | Active monitored Windows endpoint for Wazuh agent enrollment and event generation |
| Linux Endpoint 1 | Endpoint VM | Lab | Ubuntu Desktop 24.04.4 | 10.10.10.30 | Active monitored Linux endpoint for Wazuh agent enrollment and log collection |
| Kali VM | Supplemental Lab VM | Separate | Kali Linux 2026.1 (VirtualBox) | TBD | Separate VirtualBox VM used for supplemental learning/testing and not part of the primary Hyper-V Phase 1 architecture |

## Environment Notes
- The lab is being built within a personal/home network.
- Phase 1 uses Hyper-V virtual machines rather than separate physical hardware.
- The active lab design uses an Internal Hyper-V switch with NAT.
- The lab subnet is 10.10.10.0/24 and is intentionally separate from the host’s normal network.
- Guest systems use static IP configuration because the Internal NAT design does not provide DHCP.
- The host-side NAT gateway may not respond to ICMP echo from guest systems even when outbound connectivity and DNS are functioning normally.
- A separate Kali Linux VM exists in VirtualBox outside the main Hyper-V Phase 1 build.

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
| Available Storage for Lab | Variable; tracked periodically |
| Virtualization Support Enabled in BIOS | Yes |
| Preferred Virtualization Platform | Hyper-V |

## Notes
- The lab host is used to run the Phase 1 virtual machines.
- Resource allocation remains conservative because host storage is limited.
- Hyper-V was enabled successfully and verified after host restart.
