# Network Inventory

## Purpose
This document tracks the systems, devices, and network roles involved in Blue Lab. It is intended to separate personal/home infrastructure from lab infrastructure and provide a clear reference for future deployment and troubleshooting.

## Device Inventory

| Device Name | Role | Environment | OS / Platform | IP Address | Notes |
|---|---|---|---|---|---|
| Home Router | Router / Gateway | Home | eero OS | 192.168.4.1 | Main internet gateway |
| Main PC / Laptop | Lab Host | Home | Windows 11 Pro | 192.168.5.98 | Candidate machine for virtualization and lab setup |
| Windows Endpoint 1 | Planned Lab Endpoint | Lab | Windows | TBD | Will be used for Wazuh agent and event generation |
| Linux Endpoint 1 | Planned Lab Endpoint | Lab | Linux | TBD | Will be used for Wazuh agent and log collection |
| Monitoring Server | Planned Lab Server | Lab | Ubuntu Server | TBD | Intended host for central monitoring platform |

## Environment Notes
- The lab is being planned within a personal/home network.
- The first phase will likely use virtual machines rather than separate physical hardware.
- IP addresses and final host details will be added once the lab host is selected.

## Questions / Unknowns
- What virtualization platform will be used?
- Will the lab remain fully virtual for Phase 1?
- How much RAM and storage can be dedicated to the lab?

## Lab Host Specifications

| Field | Value |
|---|---|
| Host Device Name | Mr-Yeet |
| Host Operating System | Windows 11 Pro |
| CPU Model | Ryzen 9 9950X3D |
| Number of CPU Cores / Threads | 16 Cores / 32 Threads |
| RAM | 32 GB of DDR5 at 6400 MTs |
| Available Storage for Lab | 200 GB |
| Virtualization Support Enabled in BIOS | Yes |
| Preferred Virtualization Platform | VirtualBox |

## Notes
- The lab host will be used to run the initial virtual machines for Phase 1.
- Resource availability will determine how many systems can run comfortably at one time.
