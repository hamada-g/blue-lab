# Network Inventory

## Purpose
This document tracks the systems, devices, and network roles involved in Blue Lab. It is intended to separate personal/home infrastructure from lab infrastructure and provide a clear reference for future deployment and troubleshooting.

## Device Inventory

| Device Name | Role | Environment | OS / Platform | IP Address | Notes |
|---|---|---|---|---|---|
| Home Router | Router / Gateway | Home | eero OS | 192.168.4.1 | Main internet gateway |
| Main PC / Laptop | Lab Host | Home | Windows 11 Pro | 192.168.5.98 | Candidate machine for virtualization and lab setup |
| Host Internal NAT Adapter | Internal Lab Gateway | Lab | Hyper-V vEthernet | 10.10.10.1 | Gateway for Blue Lab NAT network |
| Windows Endpoint 1 | Planned Lab Endpoint | Lab | Windows | 10.10.10.20 | Will be used for Wazuh agent and event generation |
| Linux Endpoint 1 | Planned Lab Endpoint | Lab | Linux | 10.10.10.30 | Will be used for Wazuh agent and log collection |
| Monitoring Server | Planned Lab Server | Lab | Ubuntu Server | 10.10.10.10 | Intended host for central monitoring platform |

## Environment Notes
- The lab is being built within a personal/home network.
- The first phase uses virtual machines rather than separate physical hardware.
- The original External switch design was revised because it disrupted host Wi-Fi connectivity.
- Phase 1 now uses an Internal Hyper-V switch with NAT.
- The planned lab subnet is 10.10.10.0/24 to avoid overlap with the host’s home network.
- The host’s existing IP address and reserved port range on 192.168.5.98 must remain unchanged.

## Questions / Unknowns
- Should the Linux endpoint use Ubuntu Desktop or Ubuntu Server?
- What is the cleanest way to document static guest network configuration across all VMs?
- What exact order should the remaining VMs be created in?

## Lab Host Specifications

| Field | Value |
|---|---|
| Host Device Name | Mr-Yeet |
| Host Operating System | Windows 11 Pro |
| CPU Model | Ryzen 9 9950X3D |
| Number of CPU Cores / Threads | 16 Cores / 32 Threads |
| RAM | 32 GB DDR5 at 6400 MT/s |
| Available Storage for Lab | 200 GB |
| Virtualization Support Enabled in BIOS | Yes |
| Preferred Virtualization Platform | Hyper-V |

## Notes
- The lab host is used to run the initial virtual machines for Phase 1.
- Resource availability will determine how many systems can run comfortably at one time.
- Hyper-V was enabled successfully and verified after host restart.
