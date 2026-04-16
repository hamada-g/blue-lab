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
- Completed the Ubuntu installation and reached the login prompt
- Logged into the wazuh-server VM
- Verified that internet connectivity by IP and DNS resolution were working from the guest OS
- Observed that ping to the host-side NAT gateway (10.10.10.1) failed despite working outbound connectivity
- Updated the Ubuntu system and installed basic utilities successfully
- Verified hostname configuration and DNS resolution for package sources
- Installed prerequisite packages needed for Wazuh setup
- Added the Wazuh package repository
- Attempted to install package `wazuh` and received “unable to locate package”
- Confirmed that the correct package name for the server manager component is `wazuh-manager`
- Installed `wazuh-manager` successfully
- Verified that the Wazuh manager service is active and confirmed listener activity on TCP 1514
- Confirmed the server retained correct IP addressing and outbound connectivity after manager installation

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
- Ubuntu Server 24.04.4 LTS was selected as the base operating system for the Wazuh server.
- OpenSSH was selected during initial OS setup for future administration.
- Because the Internal NAT design does not provide DHCP, guest IPs are configured manually.
- The project can proceed even though the host-side NAT gateway does not respond to ping, because outbound internet access and DNS resolution from the guest are working.
- The correct Wazuh manager package name for this install path is `wazuh-manager`, not `wazuh`.

### Questions / Unknowns
- At what point should the old BlueLab-External switch be removed?
- What logging enhancements should be added to the Windows endpoint after base OS setup?
- What is the cleanest sequence for installing and validating the Wazuh agent on Windows?
- When should the Linux endpoint VM be built relative to Windows agent enrollment?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built.
- The wazuh-server VM initially failed to boot from the Ubuntu ISO due to an incompatible Secure Boot template in Hyper-V.
- The External Hyper-V switch caused host Wi-Fi connectivity loss, making it unsuitable for the Phase 1 design.
- DHCP failed during Ubuntu installation on the Internal NAT network, which required manual static IP configuration.
- The guest OS could not ping the host-side NAT gateway even though outbound internet connectivity and DNS resolution worked.
- The initial package install attempt used `wazuh`, which was not available in the repository for this setup.

### Next Step
Move on to endpoint VM creation after confirming the Wazuh server remains stable.

## 2026-04-08

### Objective
Re-verify the health of the Wazuh server before moving on to endpoint VM creation.

### Actions Taken
- Logged back into the `wazuh-server` VM
- Verified that the `wazuh-manager` service is active
- Confirmed Wazuh-related processes are present
- Reconfirmed IP addressing and routing
- Reconfirmed outbound connectivity and DNS resolution
- Reconfirmed listener activity on TCP 1514
- Updated Wazuh installation documentation to reflect the current verified state

### Decisions Made
- The Wazuh server will be treated as stable enough to proceed to endpoint VM creation once all checks pass

### Problems Encountered
- None during the re-verification step

### Next Step
Create the Windows endpoint VM and prepare it for agent installation.

## 2026-04-13

### Objective
Resume Phase 1 endpoint work and continue setup of the Windows endpoint VM.

### Actions Taken
- Confirmed the Wazuh server remains healthy enough to proceed
- Standardized the installation media path for the project as `C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media`
- Collected and organized current installation media, including:
  - `kali-linux-2026.1-installer-amd64`
  - `ubuntu-24.04.4-desktop-amd64`
  - `ubuntu-24.04.4-live-server-amd64`
  - `Win11_25H2_EnglishInternational_x64_v2`
  - `wazuh-agent-4.14.4-1`
- Created the Windows endpoint VM `win-endpoint-01`
- Assigned the VM to the BlueLab-Internal switch
- Configured the VM as Generation 2 with 8 GB RAM, 4 vCPU, and a 64 GB dynamically expanding VHDX
- Attached the Windows 11 English International 64-bit ISO
- Started Windows 11 setup in VMConnect
- Reached the OOBE network requirement screen without internet access
- Determined that the issue was expected because the VM is attached to the BlueLab-Internal NAT network without DHCP
- Used `OOBE\BYPASSNRO` to continue setup using limited configuration
- Built a separate Kali Linux VM in VirtualBox for supplemental learning and testing
- Chose to use the Hyper-V Windows 11 lab guide by jwnfld3 as a supplemental reference for VM creation and setup flow, while adapting the steps to Blue Lab requirements

### Decisions Made
- The first monitored endpoint will be a dedicated Windows 11 VM named `win-endpoint-01`
- The Windows endpoint computer name should match the VM name and remain `win-endpoint-01`
- The Windows endpoint disk uses a 64 GB dynamically expanding VHDX to balance Windows 11 requirements with limited host storage
- Static IP configuration will be applied after reaching the Windows desktop
- Ubuntu Desktop will be the preferred Linux endpoint ISO already downloaded for later use
- The separate Kali VM will be treated as supplemental lab infrastructure rather than part of the core Hyper-V Phase 1 architecture

### Problems Encountered
- Windows 11 OOBE required an internet connection before allowing account setup
- The internal NAT lab network did not provide DHCP during setup, so the installer could not auto-configure networking

### Next Step
Finish Windows 11 setup, reach the desktop, and manually configure the static IP settings for `win-endpoint-01`.

## 2026-04-15

### Objective
Complete Windows endpoint enrollment into Wazuh and standardize agent naming.

### Actions Taken
- Installed the Wazuh Windows agent inside `win-endpoint-01`
- Configured the agent to connect to the Wazuh manager at 10.10.10.10
- Verified that the `WazuhSvc` service existed and started successfully
- Confirmed Windows agent visibility from the Wazuh server using `agent_control -l`
- Observed that the first enrollment used the default Windows hostname
- Renamed the Windows endpoint to `win-endpoint-01`
- Confirmed that a new agent entry appeared with the correct hostname
- Removed the stale `DESKTOP-S5M0R8U` agent entry after verifying the new endpoint entry

### Decisions Made
- The Windows endpoint hostname and Wazuh agent name should match the documented VM name for consistency
- Agent cleanup should be performed immediately after hostname-change re-enrollment to keep manager inventory clean

### Problems Encountered
- The initial agent enrollment used the default Windows hostname rather than the intended lab endpoint name
- The hostname change caused a second agent record to appear on the manager until the stale entry was removed

### Next Step
Create and install the Linux endpoint VM, configure its static IP settings, and prepare it for Wazuh agent enrollment.
