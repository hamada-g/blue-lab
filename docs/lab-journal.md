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
- Selected Wazuh as the preferred Phase 1 monitoring platform
- Reviewed Wazuh Windows agent deployment options
- Selected PowerShell as the preferred Windows Wazuh agent installation method
- Confirmed that Wazuh agent configuration could not be completed until the Wazuh manager/server was deployed
- Clarified that the lab should use a separate Windows VM as the monitored endpoint rather than preconfiguring the host machine as an agent target
- Revised the Phase 1 storage allocation to better fit the available SSD capacity
- Added the Phase 1 VM layout to the architecture documentation
- Created the initial External switch attempt in Hyper-V
- Bound the External switch to the host Wi-Fi adapter
- Verified that the management operating system was allowed to share the selected network adapter
- Documented the initial Hyper-V networking setup
- Downloaded the Ubuntu Server 24.04 LTS ISO
- Documented the installation media
- Created the first VM: `wazuh-server`
- Attached the Ubuntu Server ISO to `wazuh-server`
- Updated the VM build notes with the VM name, generation, memory, network, virtual disk path, and installation media path
- Attempted to boot `wazuh-server` from the Ubuntu ISO
- Encountered a Hyper-V Secure Boot template issue during initial boot
- Resolved the boot issue by changing the Secure Boot template to Microsoft UEFI Certificate Authority
- Reached the Ubuntu installer successfully
- Detected that the External Hyper-V switch design was disrupting host Wi-Fi connectivity
- Decided to redesign Phase 1 networking to use an Internal Hyper-V switch with NAT
- Preserved the host’s existing network configuration by planning a separate lab subnet
- Created the BlueLab-Internal Hyper-V switch
- Assigned 10.10.10.1/24 to the host-side vEthernet adapter for the internal lab switch
- Created a NAT network named BlueLab-NAT for the 10.10.10.0/24 lab subnet
- Confirmed that the internal NAT design was active and the host-side gateway IP was in a preferred state
- Updated Hyper-V and network inventory documentation for the Internal NAT design
- Reassigned `wazuh-server` to the BlueLab-Internal switch
- Continued the Ubuntu installation under the revised Internal NAT design
- Determined that DHCP would not work on the lab network because WinNAT does not provide DHCP
- Configured the Ubuntu installer network settings manually using the planned static IP layout
- Completed the Ubuntu installation and reached the login prompt
- Logged into the `wazuh-server` VM
- Verified that internet connectivity by IP and DNS resolution were working from the guest OS
- Observed that ping to the host-side NAT gateway (10.10.10.1) failed despite working outbound connectivity
- Updated the Ubuntu system and installed basic utilities successfully
- Verified hostname configuration and DNS resolution for package sources
- Installed prerequisite packages needed for Wazuh setup
- Added the Wazuh package repository
- Attempted to install package `wazuh` and received “unable to locate package”
- Confirmed that the correct package name for the server manager component is `wazuh-manager`
- Installed `wazuh-manager` successfully
- Verified that the Wazuh manager service was active and confirmed listener activity on TCP 1514
- Confirmed the server retained correct IP addressing and outbound connectivity after manager installation

### Decisions Made
- The project would start as a simple security monitoring lab
- The first milestone would focus on one central monitoring platform and two endpoints
- Documentation would be created from day one rather than added later
- A dedicated network inventory document would be maintained before deployment began
- Phase 1 would begin fully virtualized on the main Windows host
- The full working repository would remain private during development
- A sanitized public-facing version might be created later for portfolio use
- Sensitive hostnames, IP addresses, and personal environment details would not be exposed publicly
- Hyper-V was chosen over VirtualBox for the core Phase 1 lab because the host supports native virtualization
- The initial architecture would use one monitoring server, one Windows endpoint, and one Linux endpoint
- PowerShell would be preferred over GUI for Windows Wazuh agent deployment because it is more repeatable, documentable, and automation-friendly
- The Windows host machine would not be configured as the first monitored endpoint; a dedicated Windows VM would be used instead
- Wazuh agents would only be configured after the Wazuh server was deployed and the correct manager IP/hostname was available
- Phase 1 storage allocations were reduced to keep the lab lightweight and practical on the available SSD space
- Hyper-V would remain the active virtualization platform for Phase 1
- The original External switch design would be retired because it disrupted host Wi-Fi connectivity
- Phase 1 networking would use an Internal Hyper-V switch with NAT
- The lab subnet would be 10.10.10.0/24
- Ubuntu Server 24.04.4 LTS would be selected as the base operating system for the Wazuh server
- OpenSSH would be installed during the initial Ubuntu Server setup
- Guest IPs would be configured manually because the Internal NAT design does not provide DHCP
- The project could proceed even though the host-side NAT gateway did not respond to ping, because outbound internet access and DNS resolution from the guest were working
- The correct Wazuh manager package name for this install path is `wazuh-manager`, not `wazuh`

### Questions / Unknowns
- At what point should the deprecated External switch be fully removed from the host?
- What logging enhancements should be added to the Windows endpoint after base OS setup?
- What is the cleanest sequence for documenting and validating Wazuh agent behavior across both monitored endpoints?
- How should the eventual red-lab be segmented on top of the current blue-lab baseline?

### Problems Encountered
- A Wazuh agent installation/configuration window was opened before the Wazuh server existed, which clarified that agent deployment must occur after the manager is built
- `wazuh-server` initially failed to boot from the Ubuntu ISO due to an incompatible Secure Boot template in Hyper-V
- The External Hyper-V switch caused host Wi-Fi connectivity loss, making it unsuitable for the Phase 1 design
- DHCP failed during Ubuntu installation on the Internal NAT network, which required manual static IP configuration
- The guest OS could not ping the host-side NAT gateway even though outbound internet connectivity and DNS resolution worked
- The initial package install attempt used `wazuh`, which was not available in the repository for this setup

### Next Step
Move on to endpoint VM creation after confirming the Wazuh server remained stable.

## 2026-04-08

### Objective
Re-verify the health of the Wazuh server before moving on to endpoint VM creation.

### Actions Taken
- Logged back into the `wazuh-server` VM
- Verified that the `wazuh-manager` service was active
- Confirmed Wazuh-related processes were present
- Reconfirmed IP addressing and routing
- Reconfirmed outbound connectivity and DNS resolution
- Reconfirmed listener activity on TCP 1514
- Updated Wazuh installation documentation to reflect the current verified state

### Decisions Made
- The Wazuh server would be treated as stable enough to proceed to endpoint VM creation once all checks passed

### Problems Encountered
- None during the re-verification step

### Next Step
Create the Windows endpoint VM and prepare it for agent installation.

## 2026-04-13

### Objective
Resume Phase 1 endpoint work and continue setup of the Windows endpoint VM.

### Actions Taken
- Confirmed the Wazuh server remained healthy enough to proceed
- Standardized the installation media path for the project as `C:\Lab\Blue-Lab\Installation Media`
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
- Determined that the issue was expected because the VM was attached to the BlueLab-Internal NAT network without DHCP
- Used `OOBE\BYPASSNRO` to continue setup using limited configuration
- Built a separate Kali Linux VM in VirtualBox for supplemental learning and testing
- Chose to use the Hyper-V Windows 11 lab guide by jwnfld3 as a supplemental reference for VM creation and setup flow, while adapting the steps to Blue Lab requirements

### Decisions Made
- The first monitored endpoint would be a dedicated Windows 11 VM named `win-endpoint-01`
- The Windows endpoint computer name should match the VM name and remain `win-endpoint-01`
- The Windows endpoint disk would use a 64 GB dynamically expanding VHDX to balance Windows 11 requirements with limited host storage
- Static IP configuration would be applied after reaching the Windows desktop
- Ubuntu Desktop would be the preferred Linux endpoint ISO already downloaded for later use
- The separate Kali VM would be treated as supplemental lab infrastructure rather than part of the core Hyper-V Phase 1 architecture

### Problems Encountered
- Windows 11 OOBE required an internet connection before allowing account setup
- The internal NAT lab network did not provide DHCP during setup, so the installer could not auto-configure networking

### Next Step
Finish Windows 11 setup, reach the desktop, and manually configure the static IP settings for `win-endpoint-01`.

## 2026-04-15

### Objective
Complete Windows endpoint enrollment into Wazuh, standardize agent naming, and reduce unnecessary VM resource pressure.

### Actions Taken
- Continued Windows 11 setup on `win-endpoint-01`
- Used `win-endpoint-01` as the device/computer name
- Completed Windows 11 setup with a local account
- Reached the Windows desktop successfully
- Configured a static IPv4 address on the BlueLab-Internal NAT network
- Set the Windows endpoint IP to 10.10.10.20 with gateway 10.10.10.1 and public DNS servers
- Verified local network configuration and tested outbound connectivity
- Installed the Wazuh Windows agent inside `win-endpoint-01`
- Configured the agent to connect to the Wazuh manager at 10.10.10.10
- Verified that the `WazuhSvc` service existed and started successfully
- Confirmed Windows agent visibility from the Wazuh server using `agent_control -l`
- Observed that the first enrollment used the default Windows hostname
- Renamed the Windows endpoint to `win-endpoint-01`
- Confirmed that a new agent entry appeared with the correct hostname
- Removed the stale default-hostname agent entry after verifying the new endpoint entry
- Reviewed current VM memory usage on the host
- Reduced the planned baseline memory for `wazuh-server` from 8 GB to 4 GB
- Reduced the planned baseline memory for `win-endpoint-01` from 8 GB to 4 GB
- Reduced the planned baseline memory for `linux-endpoint-01` from 4 GB to 3 GB
- Updated architecture and VM build documentation to reflect the lighter resource plan

### Decisions Made
- The Windows endpoint hostname and Wazuh agent name should match the documented VM name for consistency
- Agent cleanup should be performed immediately after hostname-change re-enrollment to keep manager inventory clean
- Static IP configuration would continue to be used on the Windows endpoint because the Internal NAT design does not provide DHCP
- The Windows endpoint would use 4 GB RAM because it is serving as a monitored lab workstation rather than a performance-focused daily-use system
- The Wazuh server would use 4 GB RAM because the current build is manager-only and does not yet include the full dashboard/indexer stack
- The planned Linux endpoint would use 3 GB RAM to preserve host memory while remaining usable

### Problems Encountered
- The initial agent enrollment used the default Windows hostname rather than the intended lab endpoint name
- The hostname change caused a second agent record to appear on the manager until the stale entry was removed
- Host resource pressure made the original memory allocations unnecessarily heavy for the current lab stage

### Next Step
Create and install the Linux endpoint VM, configure its static IP settings, and prepare it for Wazuh agent enrollment.

## 2026-04-16

### Objective
Complete the Linux endpoint build and finish the blue-lab core with three active systems.

### Actions Taken
- Completed Ubuntu Desktop installation on `linux-endpoint-01`
- Encountered a post-install keyboard/input issue at the login screen
- Resolved the keyboard/input issue by powering the VM off and back on
- Applied manual static network configuration to the Linux endpoint
- Initially misconfigured `1.1.1.1` as a local interface address instead of using it only as DNS
- Corrected the Linux network configuration and restored proper outbound connectivity
- Verified that the host-side NAT gateway still did not respond to ping, while internet and DNS remained functional
- Attempted a manual package-download approach for the Wazuh Linux agent and encountered package access issues
- Switched to the official Wazuh repo-based deployment method for Linux agents
- Installed prerequisite packages required for repo-based Wazuh deployment
- Added the Wazuh repository and imported the signing key
- Installed the Wazuh Linux agent using deployment variables
- Configured the agent name as `linux-endpoint-01`
- Enabled and started the `wazuh-agent` service
- Verified Linux agent visibility from the Wazuh server using `agent_control -l`

### Decisions Made
- The blue-lab core is now considered fully stood up with one manager and two monitored endpoints
- The deprecated External-switch attempt will be treated as historical troubleshooting context rather than part of the active architecture description
- Official Wazuh documentation should be preferred over fallback package-download methods when documenting Linux agent deployment

### Problems Encountered
- Post-install Ubuntu Desktop login-screen keyboard/input issue
- Temporary Linux network misconfiguration that incorrectly assigned `1.1.1.1` as a local IP
- Manual Wazuh Linux package-download method produced errors and was replaced with the official repo-based method
- Host-side NAT gateway still did not respond to ping even though outbound connectivity was working

### Important Commands Used
- `ip addr`
- `ip route`
- `ping -c 4 8.8.8.8`
- `ping -c 4 google.com`
- `sudo apt-get update`
- `sudo apt-get install -y curl gnupg apt-transport-https`
- `curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import`
- `echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list`
- `sudo WAZUH_MANAGER="10.10.10.10" WAZUH_AGENT_NAME="linux-endpoint-01" apt-get install -y wazuh-agent`
- `sudo systemctl enable wazuh-agent`
- `sudo systemctl start wazuh-agent`
- `sudo systemctl status wazuh-agent --no-pager`
- `sudo /var/ossec/bin/agent_control -l`

### Next Step
Stabilize and tidy the final blue-lab documentation, then begin designing the red-lab extension using the current environment as the defensive baseline.

## 2026-04-17

### Objective
Begin Phase 2A telemetry validation on the Windows endpoint and improve manager-side event visibility for readable monitoring checks.

### Actions Taken
- Began Windows telemetry baseline work on `win-endpoint-01`
- Confirmed the `WazuhSvc` service was running
- Confirmed `win-endpoint-01` remained connected on the Wazuh manager using `agent_control -l`
- Identified that the endpoint was running Windows 11 Home, which meant Group Policy Editor was not available by default
- Enabled Group Policy Editor manually through elevated Command Prompt using DISM package-addition commands before revisiting advanced audit policy configuration
- Enabled Windows process creation auditing
- Enabled command-line inclusion for process creation events
- Enabled key logon, logoff, special logon, and account-management auditing categories
- Enabled PowerShell module logging and script block logging
- Added `*`, `Microsoft.PowerShell.*`, and `Microsoft.WSMan.Management` to module logging configuration
- Confirmed Task Scheduler Operational logging
- Confirmed Windows Defender Operational logging
- Generated initial benign test activity from the Windows endpoint
- Enabled Wazuh archive logging on the manager to support raw event review during telemetry validation
- Restarted `wazuh-manager` after archive logging changes
- Confirmed that events from `win-endpoint-01` were reaching manager-side archive data
- Observed that manager-side activity from `wazuh-server` could dominate terminal output during testing and make alert-only review less useful
- Determined that SSH access from the Windows host to `wazuh-server` was preferable to using the limited Hyper-V console for archive review
- Switched to a host-side SSH workflow for manager inspection
- Selected `jq` as the preferred tool to make JSON archive output readable during validation
- Validated readable archive output from `win-endpoint-01` using host-side SSH and `jq`
- Confirmed archive collection of Windows Security and System channel events from the endpoint
- Observed sample Security event `5379` entries related to Credential Manager reads
- Observed sample System event `7040` for a service startup type change, which mapped to a Wazuh rule
- Observed sample Windows Update Client event `19` showing successful update installation
- Determined that the initial `Get-Process | Select-Object -First 5` test did not produce a clean, isolated process-creation validation in the sampled output
- Identified a mismatch between intended local audit policy and effective audit policy for process creation
- Verified that `auditpol` still showed `Process Creation` as `No Auditing` even though the advanced audit setting had been configured in Local Group Policy
- Corrected the effective process creation audit setting and revalidated Windows Security event ID `4688`
- Confirmed manager-side archive output for `win-endpoint-01` now included Security event `4688` process-creation telemetry
- Observed sample new process events including `taskhostw.exe`, `RuntimeBroker.exe`, and `sppsvc.exe`

### Decisions Made
- Phase 2A should focus first on Windows telemetry validation before moving to Linux baseline work
- Raw archive review is more useful than alert-only review during early telemetry validation
- Manager inspection should be performed over SSH from the Windows host when practical
- JSON event output should be filtered and formatted for readability rather than reviewed directly in long raw terminal streams
- Explicit process-launch tests are preferable to `Get-Process` when validating process creation visibility
- Effective audit policy must be verified with `auditpol`, not assumed from Group Policy configuration alone
- Windows edition details matter operationally and should be documented when they directly affect tooling availability or troubleshooting flow

### Problems Encountered
- Raw `alerts.json` and `archives.json` output was difficult to read in the small Hyper-V console window
- Manager-side `sudo` and other local activity on `wazuh-server` appeared prominently during testing and made quick visual review noisy
- Initial SSH access was attempted from the Windows endpoint instead of the Windows host, which was less useful for managing terminal space and workflow
- Grep-based review of JSON output was technically functional but not comfortable for sustained manual inspection without additional formatting
- The first process-related validation test did not cleanly isolate a process creation event in the sampled archive view, even though raw endpoint telemetry collection was confirmed
- Intended policy settings in Local Group Policy did not initially match the effective `auditpol` state for process creation
- Group Policy Editor was not available by default because the endpoint was running Windows 11 Home

### Important Commands Used
- `Get-Service WazuhSvc`
- `gpupdate /force`
- `auditpol /get /subcategory:"Process Creation"`
- `auditpol /set /subcategory:"Process Creation" /success:enable`
- `FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")`
- `FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")`
- `sudo /var/ossec/bin/agent_control -l`
- `sudo nano /var/ossec/etc/ossec.conf`
- `sudo systemctl restart wazuh-manager`
- `ssh blueadmin@10.10.10.10`
- `sudo apt-get update && sudo apt-get install -y jq`
- `sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | tail -n 10 | jq '{timestamp, agent: .agent.name, location: .location, decoder: .decoder.name, rule: (.rule.description // "no rule"), full_log}'`
- `sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | grep -a '"location":"EventChannel"' | tail -n 10 | jq '{timestamp, agent: .agent.name, location: .location, decoder: .decoder.name, rule: (.rule.description // "no rule"), full_log}'`
- `sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | jq 'select(.location=="EventChannel") | .full_log |= fromjson | select(.full_log.win.system.eventID=="4688" or (.full_log.win.system.providerName | test("PowerShell"))) | {timestamp, agent: .agent.name, eventID: .full_log.win.system.eventID, provider: .full_log.win.system.providerName, channel: .full_log.win.system.channel, message: .full_log.win.system.message}'`
- `sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | jq 'select(.location=="EventChannel") | .full_log |= fromjson | select(.full_log.win.system.eventID=="4688") | {timestamp, agent: .agent.name, eventID: .full_log.win.system.eventID, provider: .full_log.win.system.providerName, channel: .full_log.win.system.channel, message: .full_log.win.system.message}'`

### Next Step
Continue Phase 2A by validating PowerShell logging, failed logon visibility, local account management events, and scheduled task activity on `win-endpoint-01` before moving on to Linux telemetry baseline work.
