# Network Inventory

## Purpose
This document tracks the systems, devices, and network roles involved in Blue Lab. It is intended to separate personal/home infrastructure from lab infrastructure and provide a clear reference for future deployment and troubleshooting.

## Device Inventory

| Device Name | Role | Environment | OS / Platform | IP Address | Notes |
|---|---|---|---|---|---|
| Home Router | Router / Gateway | Home | eero OS | 192.168.4.1 | Main internet gateway |
| Main PC / Laptop | Lab Host | Home | Windows 11 Pro | 192.168.5.98 | Host system for Hyper-V lab |
| Host Internal NAT Adapter | Internal Lab Gateway | Lab | Hyper-V vEthernet | 10.10.10.1 | Gateway for Blue Lab NAT network |
| Monitoring Server | Lab Server | Lab | Ubuntu Server | 10.10.10.10 | Wazuh manager host |
| Windows Endpoint 1 | Endpoint VM | Lab | Windows 11 | 10.10.10.20 | Active monitored Windows endpoint for Wazuh agent enrollment and event generation |
| Linux Endpoint 1 | Planned Endpoint VM | Lab | Ubuntu Desktop | 10.10.10.30 | Planned monitored Linux endpoint for Wazuh agent enrollment and log collection |
| Kali VM | Supplemental Lab VM | Separate | Kali Linux (VirtualBox) | TBD | Separate VirtualBox VM used for supplemental learning/testing and not part of primary Hyper-V Phase 1 architecture |

## Environment Notes
- The lab is being built within a personal/home network.
- Phase 1 uses Hyper-V virtual machines rather than separate physical hardware.
- The original External switch design was revised because it disrupted host Wi-Fi connectivity.
- Phase 1 now uses an Internal Hyper-V switch with NAT.
- The planned lab subnet is 10.10.10.0/24 to avoid overlap with the host’s home network.
- The host’s existing IP address and reserved port range on 192.168.5.98 must remain unchanged.
- Guest systems use static IP configuration because the Internal NAT design does not provide DHCP.
- A separate Kali Linux VM exists in VirtualBox outside the main Hyper-V Phase 1 build.

## Questions / Unknowns
- At what point should the old BlueLab-External switch be removed?
- What logging enhancements should be added to the Windows endpoint after base OS setup?
- What is the cleanest sequence for installing and validating the Wazuh agent on Windows?
- When should the Linux endpoint VM be built relative to Windows agent enrollment?
- Should the Kali VM eventually be documented in a separate supplemental-lab section rather than the core Phase 1 docs?

## Lab Host Specifications

| Field | Value |
|---|---|
| Host Device Name | Mr-Yeet |
| Host Operating System | Windows 11 Pro |
| CPU Model | Ryzen 9 9950X3D |
| Number of CPU Cores / Threads | 16 Cores / 32 Threads |
| RAM | 32 GB DDR5 at 6400 MT/s |
| Available Storage for Lab | ~219 GB free as of 2026-04-13 |
| Virtualization Support Enabled in BIOS | Yes |
| Preferred Virtualization Platform | Hyper-V |

## Notes
- The lab host is used to run the Phase 1 virtual machines.
- Resource allocation must remain conservative because host storage is limited.
- Hyper-V was enabled successfully and verified after host restart.
