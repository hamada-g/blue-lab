# Hyper-V Setup

## Active Hyper-V Design

### Internal Switch
- Switch Name: `BlueLab-Internal`
- Switch Type: Internal

### Lab Subnet
- Network: `10.10.10.0/24`
- Host Gateway IP: `10.10.10.1`

### NAT Configuration
- NAT Name: `BlueLab-NAT`
- Internal Prefix: `10.10.10.0/24`
- Status: Active

## Notes
- The active Blue Lab Phase 1 network uses an Internal Hyper-V switch with host-provided NAT.
- The host remains on its normal network while also providing NAT for the lab VMs.
- The lab subnet is intentionally separate from the host’s primary network.
- All active Phase 1 VMs are attached to `BlueLab-Internal`.
- DHCP is not provided by this design, so guest systems use static IP configuration.

## Historical Troubleshooting Context

### Historical External Switch Attempt
- Switch Name: `BlueLab-External`
- Switch Type: External
- Host Adapter Used: Host Wi-Fi adapter

### Historical Notes
- This was the first switch design attempted for Blue Lab Phase 1.
- This design caused host Wi-Fi connectivity issues and was abandoned.
- It is preserved here only as historical troubleshooting context.
- It is not part of the active architecture.
