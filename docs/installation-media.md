# Installation Media

## Ubuntu Server ISO

### Purpose
This ISO will be used to create the Phase 1 Wazuh server virtual machine.

### Selected OS
Ubuntu Server 24.04 LTS

### Architecture
64-bit AMD64

### Planned VM
wazuh-server

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media

### Notes
- Ubuntu Server 24.04 LTS was selected because it is a current long-term support release.
- Wazuh supports Ubuntu 24.04 for server installation.
- This ISO will be attached to the first VM created in Hyper-V.
- The original External switch design was revised because it disrupted host Wi-Fi connectivity.
- Phase 1 will instead use an Internal Hyper-V switch with NAT.
- The planned lab subnet will be 10.10.10.0/24 to avoid overlap with the host’s home network.
- The host’s existing IP address and reserved port range on 192.168.5.98 must remain unchanged.
