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
- Hyper-V is now the active virtualization platform for Phase 1

### Questions / Unknowns
- What internal IP range or naming scheme should be used for the VMs?
- Should the Linux endpoint use Ubuntu Desktop or Ubuntu Server?
- What is the cleanest way to document Hyper-V setup and switch configuration?
- What exact order should the VMs be created in?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built

### Next Step
Create the Hyper-V virtual networking setup and document how the lab VMs will communicate.
