# Installation Media

## Base Media Directory
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media

## Current Files Present
- kali-linux-2026.1-installer-amd64
- ubuntu-24.04.4-desktop-amd64
- ubuntu-24.04.4-live-server-amd64
- Win11_25H2_EnglishInternational_x64_v2
- wazuh-agent-4.14.4-1

## Ubuntu Server ISO

### Purpose
This media is used to create the Phase 1 Wazuh server virtual machine.

### Selected OS
Ubuntu Server 24.04.4 LTS

### Planned / Actual VM
wazuh-server

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\ubuntu-24.04.4-live-server-amd64

### Notes
- Ubuntu Server 24.04.4 LTS was selected because it is a current long-term support release.
- This media was used to build the first VM in the lab.

## Windows 11 ISO

### Purpose
This media is used to create the Phase 1 Windows endpoint virtual machine.

### Selected OS
Windows 11 English International 64-bit

### Planned / Actual VM
win-endpoint-01

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\Win11_25H2_EnglishInternational_x64_v2

### Notes
- This media is attached to the Windows endpoint VM in Hyper-V.
- The Windows endpoint will later be configured with a static IP on the BlueLab-Internal NAT network.
- The Windows endpoint install is currently in progress.

## Ubuntu Desktop ISO

### Purpose
This media will be used to create the Phase 1 Linux endpoint virtual machine.

### Selected OS
Ubuntu Desktop 24.04.4

### Planned VM
linux-endpoint-01

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\ubuntu-24.04.4-desktop-amd64

### Notes
- Ubuntu Desktop was selected to provide a more usable Linux endpoint experience in the lab.
- The Linux endpoint will later be configured with a static IP on the BlueLab-Internal NAT network.
- This media has been downloaded but not used yet.

## Kali Installer

### Purpose
This media is used for a separate Kali Linux virtual machine in VirtualBox.

### Selected OS
Kali Linux 2026.1

### VM
Separate VirtualBox Kali VM

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\kali-linux-2026.1-installer-amd64

### Notes
- This Kali VM is not part of the primary Blue Lab Phase 1 Hyper-V architecture.
- It is used as a supplemental VM for learning and testing.

## Wazuh Agent MSI

### Purpose
This installer will be used for future Wazuh agent installation on the Windows endpoint.

### Planned VM
win-endpoint-01

### Local File Path
C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\wazuh-agent-4.14.4-1

### Notes
- This file is staged in advance to reduce dependency on future downloads during endpoint configuration.
- Although the Wazuh MSI was staged on the host in the installation media directory, the actual Windows endpoint installation used a guest-side download because the Hyper-V VM did not have direct access to host files during setup.
