# VM Build Notes

## wazuh-server

### VM Purpose
This virtual machine hosts the central Wazuh monitoring platform for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: `wazuh-server`
- Generation: Generation 2
- Memory: 4096 MB
- Processor: 4 vCPU
- Network: `BlueLab-Internal`
- Hard Disk: `<Hyper-V Virtual Disks>\wazuh-server.vhdx` (VHDX, dynamically expanding)
- Operating System: Ubuntu Server 24.04.4 LTS

### Notes
- This was the first VM created for Blue Lab Phase 1.
- The operating system installation was completed successfully.
- The VM initially booted under an earlier network design and was later reassigned to `BlueLab-Internal`.
- Wazuh manager is installed and active on this VM.

---

## win-endpoint-01

### VM Purpose
This virtual machine serves as the monitored Windows endpoint for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: `win-endpoint-01`
- Generation: Generation 2
- Memory: 4096 MB
- Processor: 4 vCPU
- Network: `BlueLab-Internal`
- Hard Disk: 64 GB VHDX (dynamically expanding)
- Operating System: Windows 11 English International 64-bit
- Computer Name: `win-endpoint-01`

### Network Configuration
- Static IP: `10.10.10.20`
- Subnet: `10.10.10.0/24`
- Gateway: `10.10.10.1`
- DNS: `1.1.1.1`, `8.8.8.8`

### Notes
- Windows 11 setup completed successfully and the desktop was reached.
- The Wazuh Windows agent was installed and enrolled to the Wazuh manager.
- The endpoint was renamed to `win-endpoint-01` after the initial enrollment.
- The stale initial agent entry using the default Windows hostname was removed from the manager.

---

## linux-endpoint-01

### VM Purpose
This virtual machine serves as the monitored Linux endpoint for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: `linux-endpoint-01`
- Generation: Generation 2
- Memory: 3072 MB
- Processor: 2 vCPU
- Network: `BlueLab-Internal`
- Hard Disk: 25 GB VHDX (dynamically expanding)
- Operating System: Ubuntu Desktop 24.04.4
- Computer Name: `linux-endpoint-01`

### Network Configuration
- Static IP: `10.10.10.30`
- Subnet: `10.10.10.0/24`
- Gateway: `10.10.10.1`
- DNS: `1.1.1.1`, `8.8.8.8`

### Notes
- Ubuntu Desktop installation completed successfully.
- The VM initially experienced a post-install keyboard/input issue at the login screen, which was resolved by rebooting the VM.
- A network configuration mistake briefly assigned `1.1.1.1` as a local address instead of using it only as DNS; this was corrected.
- The Linux Wazuh agent was installed and enrolled successfully to the Wazuh manager.

---

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
