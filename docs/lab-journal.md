# Lab Journal

## 2026-04-02

### Objective
Start the Blue Lab project with proper structure and documentation.

### Actions Taken
- Created the GitHub repository
- Added the initial folder structure
- Created the core documentation files
- Wrote the project charter
- Created the initial network inventory document
- Recorded the home router as the main internet gateway
- Identified the main lab host as a Windows 11 Pro system on the home network
- Documented the lab host hardware specifications, available storage, and virtualization readiness
- Chose Hyper-V as the preferred virtualization platform for Phase 1
- Enabled Hyper-V through Windows Features
- Restarted the host system to activate Hyper-V
- Verified that Hyper-V was available after reboot
- Created the initial Phase 1 architecture document
- Selected Wazuh as the Phase 1 monitoring platform
- Reviewed Wazuh Windows agent deployment options
- Selected PowerShell as the preferred Windows agent installation method for future deployment
- Confirmed that Wazuh agent configuration cannot be completed until the Wazuh manager/server is deployed
- Clarified that the lab should use a separate Windows VM as the monitored endpoint rather than preconfiguring the host machine as an agent target
- Revised the Phase 1 storage allocation to better fit the available SSD capacity
- Added the Phase 1 VM layout to the architecture documentation
- Created the BlueLab-External virtual switch in Hyper-V
- Bound the external switch to the Realtek 8922AE WiFi 7 PCI-E NIC
- Verified that the management operating system was allowed to share the selected network adapter
- Documented the initial Hyper-V networking setup
- Downloaded the Ubuntu Server 24.04 LTS ISO
- Documented the installation media
- Created the first VM: wazuh-server
- Attached the Ubuntu Server ISO to the wazuh-server VM
- Updated the VM build notes with the exact VM name, generation, memory, network, virtual disk path, and installation media path
- Attempted to boot the wazuh-server VM from the Ubuntu ISO
- Encountered a Hyper-V Secure Boot template issue during initial boot
- Resolved the boot issue by changing the Secure Boot template to Microsoft UEFI Certificate Authority
- Reached the Ubuntu installer successfully
- Detected that the External Hyper-V switch design was disrupting host Wi-Fi connectivity
- Decided to redesign Phase 1 networking to use an Internal Hyper-V switch with NAT
- Preserved the host’s existing network identity and port reservation requirements by planning a separate lab subnet
- Created the BlueLab-Internal Hyper-V switch
- Assigned 10.10.10.1/24 to the host-side vEthernet adapter for the internal lab switch
- Created a NAT network named BlueLab-NAT for the 10.10.10.0/24 lab subnet
- Confirmed that the internal NAT design is active and the host-side gateway IP is in a preferred state
- Updated Hyper-V and network inventory documentation for the Internal NAT design
- Reassigned the wazuh-server VM to the BlueLab-Internal switch
- Continued the Ubuntu installation under the revised Internal NAT design
- Determined that DHCP would not work on the lab network because WinNAT does not provide DHCP
- Configured the Ubuntu installer network settings manually using the planned static IP layout

### Decisions Made
- The project will start as a simple security monitoring lab.
- The first milestone will focus on one central monitoring platform and two endpoints.
- Documentation will be created from day one rather than added later.
- A dedicated network inventory document will be maintained before deployment begins.
- Phase 1 will begin fully virtualized on the main Windows host.
- The full working repository will remain private during development.
- A sanitized public-facing version may be created later for portfolio use.
- Sensitive hostnames, IP addresses, and personal environment details will not be exposed publicly.
- Hyper-V was chosen over VirtualBox because the host runs Windows 11 Pro and supports native virtualization.
- The initial architecture will use one monitoring server, one Windows endpoint, and one Linux endpoint.
- PowerShell will be preferred over GUI for Windows Wazuh agent deployment because it is more repeatable, documentable, and automation-friendly.
- The Windows host machine will not be configured as the first monitored endpoint; a dedicated Windows VM will be used instead.
- Wazuh agents will only be configured after the Wazuh server is deployed and the correct manager IP/hostname is available.
- Phase 1 storage allocations were reduced to keep the lab lightweight and practical on the available SSD space.
- Hyper-V is the active virtualization platform for Phase 1.
- The original External switch design was retired because it disrupted host Wi-Fi connectivity.
- Phase 1 networking now uses an Internal Hyper-V switch with NAT.
- The lab subnet is 10.10.10.0/24.
- The host gateway IP on the lab subnet is 10.10.10.1.
- The host’s existing IP address and reserved port range on 192.168.5.98 remain unchanged.
- Ubuntu Server 24.04 LTS was selected as the base operating system for the Wazuh server.
- OpenSSH was selected during initial OS setup for future administration.
- Because the Internal NAT design does not provide DHCP, guest IPs are configured manually.

### Questions / Unknowns
- Should the Linux endpoint use Ubuntu Desktop or Ubuntu Server?
- What exact order should the remaining VMs be created in?
- What post-install checks should be run first on the Wazuh server?
- At what point should the old BlueLab-External switch be removed?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built.
- The wazuh-server VM initially failed to boot from the Ubuntu ISO due to an incompatible Secure Boot template in Hyper-V.
- The External Hyper-V switch caused host Wi-Fi connectivity loss, making it unsuitable for the Phase 1 design.
- DHCP failed during Ubuntu installation on the Internal NAT network, which required manual static IP configuration.

### Next Step
Complete the Ubuntu installation, boot into the installed operating system, and verify the Wazuh server’s network configuration from داخل the guest OS.
