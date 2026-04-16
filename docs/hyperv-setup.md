# Hyper-V Setup

## Historical External Switch Attempt

### Switch Name
BlueLab-External

### Switch Type
External

### Host Adapter Used
Host Wi-Fi adapter

### Historical Notes
- This was the first switch design attempted for Blue Lab Phase 1.
- This design caused host Wi-Fi connectivity issues and was abandoned.
- It is preserved here only as historical troubleshooting context, not as part of the active architecture.

## Current Internal NAT Design

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
- The Internal NAT design replaced the External switch approach because the External switch caused host connectivity instability.
- The host remains on its normal Wi-Fi network while also providing NAT for the lab VMs.
- The lab subnet is intentionally separate from the host’s normal network.
- All current Phase 1 VMs are attached to `BlueLab-Internal`.
