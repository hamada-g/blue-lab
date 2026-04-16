# OS Installation Notes

## wazuh-server

### Operating System
Ubuntu Server 24.04.4 LTS

### Installation Summary
- VM Name: wazuh-server
- Hostname: wazuh-server
- Username: blueadmin
- Network Design During Install: BlueLab-Internal via Hyper-V Internal NAT design
- Static IP: 10.10.10.10/24
- Gateway: 10.10.10.1
- DNS Servers: 1.1.1.1, 8.8.8.8
- Storage: Guided install using entire virtual disk
- LVM: Not enabled
- OpenSSH Server: Installed

### Notes
- Ubuntu Server was installed successfully on the first VM in Blue Lab Phase 1.
- The VM initially failed to boot due to a Secure Boot template issue in Hyper-V.
- The issue was resolved by changing the Secure Boot template to Microsoft UEFI Certificate Authority.
- The original External switch design was replaced with an Internal NAT design before completing the install.
- DHCP failed during install as expected because the Internal NAT design does not provide DHCP automatically.
- The network interface was configured manually with a static IP.
- The system is fully installed and operational.

### Post-Install Verification
- Successfully logged into the Ubuntu Server VM
- Verified static IP configuration on the lab network
- Verified default route configuration
- Verified external connectivity by IP
- Verified DNS resolution
- Ping to the host-side NAT gateway (10.10.10.1) returned 100% packet loss
- Despite gateway ping failure, outbound internet connectivity and DNS resolution were functional

### Pre-Install Preparation
- Verified hostname configuration
- Verified DNS resolution for external package sources
- Installed prerequisite packages: curl, apt-transport-https, unzip, lsb-release, gnupg
- Reconfirmed static IP and routing configuration

## win-endpoint-01

### Operating System
Windows 11 English International 64-bit

### Installation Summary
- VM Name: win-endpoint-01
- Computer Name: win-endpoint-01
- Username: blueadmin
- Network Design During Install: BlueLab-Internal via Hyper-V Internal NAT design
- Static IP: 10.10.10.20/24
- Gateway: 10.10.10.1
- DNS Servers: 1.1.1.1, 8.8.8.8
- Storage: 64 GB dynamically expanding VHDX

### Notes
- Windows 11 installation completed successfully.
- Windows OOBE required an internet connection before allowing account setup.
- Because the internal NAT design does not provide DHCP automatically, the installer could not auto-configure networking.
- The OOBE network requirement was bypassed using `OOBE\BYPASSNRO` so setup could continue using limited configuration.
- Static IP configuration was applied manually after reaching the Windows desktop.

### Post-Install Verification
- Reached the Windows desktop successfully
- Verified static IP configuration
- Verified outbound connectivity by IP
- Verified DNS resolution

### Additional Endpoint Configuration
- Installed the Wazuh Windows agent successfully
- Verified that the `WazuhSvc` service was present and running
- Confirmed agent enrollment to the Wazuh manager at `10.10.10.10`
- Renamed the endpoint to `win-endpoint-01` to match the lab naming convention
- Removed the stale initial agent record that had enrolled under the default Windows hostname

## linux-endpoint-01

### Operating System
Ubuntu Desktop 24.04.4

### Installation Summary
- VM Name: linux-endpoint-01
- Computer Name: linux-endpoint-01
- Network Design During Install: BlueLab-Internal via Hyper-V Internal NAT design
- Static IP: 10.10.10.30/24
- Gateway: 10.10.10.1
- DNS Servers: 1.1.1.1, 8.8.8.8
- Storage: 25 GB dynamically expanding VHDX

### Notes
- Ubuntu Desktop installation completed successfully.
- The VM initially experienced a login-screen keyboard/input issue after install, which was resolved by powering the VM off and back on.
- A network misconfiguration briefly assigned `1.1.1.1` as a local interface address instead of only a DNS server; this was corrected.
- Although the host-side NAT gateway did not respond to ping, outbound internet connectivity and DNS resolution worked correctly.
- The Linux Wazuh agent was installed and enrolled to the Wazuh manager at `10.10.10.10`.

### Post-Install Verification
- Verified static IP configuration
- Verified default route
- Verified outbound connectivity by IP
- Verified DNS resolution
- Verified `wazuh-agent` service status
- Verified agent visibility on the Wazuh manager
