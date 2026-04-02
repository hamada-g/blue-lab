# VM Build Notes

## wazuh-server

### VM Purpose
This virtual machine will host the central Wazuh monitoring platform for Blue Lab Phase 1.

### Hyper-V Configuration
- Name: wazuh-server
- Generation: Generation 2
- Memory: 8192 MB
- Network: BlueLab-External
- Hard Disk: C:\ProgramData\Microsoft\Windows\Virtual Hard Disks\wazuh-server.vhdx (VHDX, dynamically expanding)
- Operating System: Will be installed from C:\Users\mgami\OneDrive\Desktop\Job Application Stuff\Blue-Lab Project\Installation Media\ubuntu-24.04.4-live-server-amd64.iso

### Notes
- This is the first VM created for Blue Lab Phase 1.
- The operating system has not been installed yet.
- This VM will be installed and configured before any endpoint VMs are created.
