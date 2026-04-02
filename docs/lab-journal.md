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
- Enabled Hyper-V through Windows Features, pending restart at the appropriate setup step
- Created the initial Phase 1 architecture document
- Reviewed Wazuh Windows agent deployment options
- Selected PowerShell as the preferred Windows agent installation method for future deployment
- Confirmed that Wazuh agent configuration cannot be completed until the Wazuh manager/server is deployed
- Clarified that the lab should use a separate Windows VM as the monitored endpoint rather than preconfiguring the host machine as an agent target

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

### Questions / Unknowns
- How much RAM should be allocated to each VM?
- What exact VM layout should be used for the first milestone?
- When should the host machine be restarted to activate Hyper-V cleanly?
- What exact Wazuh installation path should be used for the central server?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built

### Next Step
Restart the host at the appropriate setup stage, confirm Hyper-V is active, and define the exact VM layout for Phase 1.
