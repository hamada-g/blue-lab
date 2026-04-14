# Installation Media

## Ubuntu Server ISO

### Purpose
This ISO is used to create the Phase 1 Wazuh server virtual machine.

### Selected OS
Ubuntu Server 24.04.4 LTS

### Architecture
64-bit AMD64

### Planned VM
wazuh-server

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\ubuntu-24.04.4-live-server-amd64.iso

### Notes
- Ubuntu Server 24.04.4 LTS was selected because it is a current long-term support release.
- This ISO was used to build the first VM in the lab.

## Windows 11 ISO

### Purpose
This ISO is used to create the Phase 1 Windows endpoint virtual machine.

### Selected OS
Windows 11 English International 64-bit

### Planned VM
win-endpoint-01

### Local File Path
TBD

### Notes
- This ISO is attached to the Windows endpoint VM in Hyper-V.
- The Windows endpoint will later be configured with a static IP on the BlueLab-Internal NAT network.
- The Windows endpoint install is currently in progress.

## Ubuntu Desktop ISO

### Purpose
This ISO will be used to create the Phase 1 Linux endpoint virtual machine.

### Selected OS
Ubuntu Desktop

### Planned VM
linux-endpoint-01

### Local File Path
TBD

### Notes
- Ubuntu Desktop was selected to provide a more usable Linux endpoint experience in the lab.
- The Linux endpoint will later be configured with a static IP on the BlueLab-Internal NAT network.
- This ISO has been downloaded but not used yet.

## Other Installation Files

### Wazuh Agent MSI
- Purpose: Future installation on `win-endpoint-01`
- Local File Path: TBD

### Codex Installer
- Purpose: Local Codex setup on the host if needed
- Local File Path: TBD
