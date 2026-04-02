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

## Design Revision
- The original BlueLab-External switch design caused host connectivity issues on Wi-Fi.
- The Phase 1 network design is being changed to use an Internal switch with NAT instead.
- The External switch may be removed or retired after the Internal NAT design is implemented successfully.

## Internal NAT Setup

### Internal Switch
- Switch Name: BlueLab-Internal
- Switch Type: Internal

### Lab Subnet
- Network: 10.10.10.0/24
- Host Gateway IP: 10.10.10.1

### NAT Configuration
- NAT Name: BlueLab-NAT
- Internal Prefix: 10.10.10.0/24
- Status: Active

### Notes
- This Internal NAT design replaced the original External switch approach because the External switch caused host Wi-Fi connectivity issues.
- The host remains on its normal Wi-Fi network while also providing NAT for the lab VMs.
- The lab subnet is intentionally separate from the host’s home network and does not interfere with the host’s reserved port range on 192.168.5.98.
