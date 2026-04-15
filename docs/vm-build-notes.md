# VM Build Notes

## wazuh-server

### VM Purpose
This virtual machine hosts the central Wazuh monitoring platform for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: wazuh-server
- Generation: Generation 2
- Memory: 4096 MB
- Network: BlueLab-Internal
- Hard Disk: C:\ProgramData\Microsoft\Windows\Virtual Hard Disks\wazuh-server.vhdx (VHDX, dynamically expanding)
- Operating System: Ubuntu Server 24.04.4 LTS

### Notes
- This is the first VM created for Blue Lab Phase 1.
- The operating system installation was completed successfully.
- The VM initially booted under the earlier network design and was later reassigned to BlueLab-Internal.
- Wazuh manager is installed and active on this VM.

## win-endpoint-01

### VM Purpose
This virtual machine serves as the monitored Windows endpoint for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: win-endpoint-01
- Generation: Generation 2
- Memory: 4096 MB
- Processor: 4 vCPU
- Network: BlueLab-Internal
- Hard Disk: 64 GB VHDX (dynamically expanding)
- Operating System: Windows 11 English International 64-bit
- Planned Computer Name: win-endpoint-01

### Planned Network Configuration
- Static IP: 10.10.10.20
- Subnet: 10.10.10.0/24
- Gateway: 10.10.10.1
- DNS: 1.1.1.1, 8.8.8.8

### Installation Notes
- Windows 11 setup reached the OOBE network requirement screen without internet access.
- This was expected because the VM is attached to the BlueLab-Internal NAT network, which does not provide DHCP automatically.
- The OOBE network requirement was bypassed using `OOBE\BYPASSNRO` so setup could continue with limited configuration.

### Notes
- This VM will be used for Windows event generation, endpoint telemetry, and Wazuh agent enrollment.
- A community Hyper-V Windows 11 lab guide was used as a supplemental reference for VM creation flow, adapted to the Blue Lab environment.
- As of 2026-04-13, Windows setup is still in progress and the desktop has not yet been fully reached.

## linux-endpoint-01

### VM Purpose
This virtual machine will serve as the monitored Linux endpoint for Blue Lab Phase 1.

### Planned Hyper-V Configuration
- Name: linux-endpoint-01
- Generation: Generation 2
- Memory: 3072 MB
- Processor: 2 vCPU
- Network: BlueLab-Internal
- Hard Disk: 25 GB VHDX (dynamically expanding)
- Operating System: Ubuntu Desktop 24.04.4

### Planned Network Configuration
- Static IP: 10.10.10.30
- Subnet: 10.10.10.0/24
- Gateway: 10.10.10.1
- DNS: 1.1.1.1, 8.8.8.8

### Notes
- This VM has not been created yet.
- It will be used for Linux log generation, authentication events, and Wazuh agent enrollment after the Windows endpoint is online.

## kali-vbox

### VM Purpose
This separate VirtualBox VM is used for supplemental Kali Linux learning and testing outside the primary Phase 1 Hyper-V architecture.

### Platform
- VirtualBox

### Operating System
- Kali Linux 2026.1

### Notes
- This VM is not part of the core Blue Lab Phase 1 monitoring architecture.
- It may later support supplemental offensive-security-oriented practice or isolated testing workflows.
