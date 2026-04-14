# Hyper-V Setup

## Original External Switch

### Switch Name
BlueLab-External

### Switch Type
External

### Host Adapter Used
Realtek 8922AE WiFi 7 PCI-E NIC

### Original Notes
- This was the first switch design attempted for Blue Lab Phase 1.
- The management operating system was allowed to share the selected network adapter.
- This design caused host Wi-Fi connectivity issues and is no longer the preferred Phase 1 networking model.

## Design Revision
- The original BlueLab-External switch design caused host connectivity issues on Wi-Fi.
- The Phase 1 network design was changed to use an Internal switch with NAT instead.
- The External switch may be removed later after the Internal NAT design is fully validated.

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
- The current Phase 1 VMs should be attached to BlueLab-Internal.
