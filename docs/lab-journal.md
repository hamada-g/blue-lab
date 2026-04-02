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
- Reviewed Wazuh Windows agent deployment options
- Selected PowerShell as the preferred Windows agent installation method for future deployment
- Confirmed that Wazuh agent configuration cannot be completed until the Wazuh manager/server is deployed
- Clarified that the lab should use a separate Windows VM as the monitored endpoint rather than preconfiguring the host machine as an agent target
- Revised the Phase 1 storage allocation to better fit the available SSD capacity
- Added the Phase 1 VM layout to the architecture documentation
- Created the BlueLab-External virtual switch in Hyper-V
- Bound the external switch to the Realtek 8922AE WiFi 7 PCI-E NIC
- Verified that the management operating system is allowed to share the selected network adapter
- Documented the initial Hyper-V networking setup

### Decisions Made
- The project will start as a simple security monitoring lab
- The first milestone will focus on one central monitoring platform and two endpoints
- Documentation will be created from day one rather than added later
- A dedicated network inventory document will be maintained before deployment begins
- Phase 1 will begin fully virtualized on the main Windows host
- The full working repository will remain private during development
- A sanitized public-facing version may be created later for portfolio use
- Sensitive hostnames, IP addresses, and personal environment details will not be exposed publicly
- Hyper-V was chosen over VirtualBox because the host runs Windows 11 Pro and supports native virtualization
- The initial architecture will use one monitoring server, one Windows endpoint, and one Linux endpoint
- PowerShell will be preferred over GUI for Windows Wazuh agent deployment because it is more repeatable, documentable, and automation-friendly
- The Windows host machine will not be configured as the first monitored endpoint; a dedicated Windows VM will be used instead
- Wazuh agents will only be configured after the Wazuh server is deployed and the correct manager IP/hostname is available
- Phase 1 storage allocations were reduced to keep the lab lightweight and practical on the available SSD space
- Hyper-V is the active virtualization platform for Phase 1
- A single external virtual switch will be used initially to keep VM networking simple and reliable

### Questions / Unknowns
- What internal IP range or naming scheme should be used for the VMs?
- Should the Linux endpoint use Ubuntu Desktop or Ubuntu Server?
- What exact order should the VMs be created in?
- Which VM should be built first?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built

### Next Step
Download and document the Ubuntu Server installation media for the Wazuh server VM.
