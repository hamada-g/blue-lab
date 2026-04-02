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

### Questions / Unknowns
- How much RAM should be allocated to each VM?
- Which monitoring platform will be deployed first?
- What exact VM layout should be used for the first milestone?
- When should the host machine be restarted to activate Hyper-V cleanly?

### Problems Encountered
- None so far

### Next Step
Create and document the initial Phase 1 architecture before beginning installation and VM planning.
