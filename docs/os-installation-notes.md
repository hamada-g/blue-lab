# OS Installation Notes

## wazuh-server

### Operating System
Ubuntu Server 24.04 LTS

### Installation Summary
- VM Name: wazuh-server
- Hostname: wazuh-server
- Username: blueadmin
- Network Design During Install: BlueLab-Internal via Hyper-V Internal NAT design
- Planned Static IP: 10.10.10.10/24
- Planned Gateway: 10.10.10.1
- Planned DNS Servers: 1.1.1.1, 8.8.8.8
- Storage: Guided install using entire virtual disk
- LVM: Not enabled
- OpenSSH Server: Installed (selected during setup)

### Notes
- Ubuntu Server is being installed on the first VM in Blue Lab Phase 1.
- The VM initially failed to boot due to a Secure Boot template issue in Hyper-V.
- The issue was resolved by changing the Secure Boot template to Microsoft UEFI Certificate Authority.
- The original External switch design was replaced with an Internal NAT design before completing the install.
- DHCP failed during install as expected because the Internal NAT design does not provide DHCP automatically.
- The network interface is being configured manually with a static IP.
- The system will be ready for post-install verification and network validation after installation completes.
