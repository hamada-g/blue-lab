# Hyper-V Setup

## Phase 1 Virtual Switch

### Switch Name
BlueLab-External

### Switch Type
External

### Purpose
This switch provides network connectivity for the Blue Lab virtual machines. It allows the lab VMs to communicate with each other and reach the internet through the host system’s active network adapter.

### Host Adapter Used
Realtek 8922AE WiFi 7 PCI-E NIC

### Important Configuration
- The management operating system is allowed to share the selected network adapter.
- This switch will be used by the Wazuh server VM, the Windows endpoint VM, and the Linux endpoint VM.

### Notes
- This is the primary external switch for Blue Lab Phase 1.
- The switch is bound to the host’s Realtek 8922AE WiFi 7 PCI-E NIC.
- The network connection may briefly reset when the switch is created.
- Phase 1 uses a simple external switch for ease of setup and connectivity.
