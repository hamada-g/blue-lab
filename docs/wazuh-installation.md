# Wazuh Installation

## wazuh-server

### Repository Setup
- Imported the Wazuh GPG signing key
- Added the Wazuh APT repository for the 4.x release line
- Updated package lists successfully

### Installation
- Initial attempt to install package `wazuh` failed because the package was not found
- Confirmed that the correct package for the manager component is `wazuh-manager`
- Installed `wazuh-manager` on Ubuntu Server 24.04.4 LTS

### Service Verification
- Enabled the `wazuh-manager` service
- Started the `wazuh-manager` service
- Verified service status with `systemctl status wazuh-manager`
- Confirmed listener activity on TCP 1514
- Verified Wazuh-related processes are present
- Reconfirmed server IP configuration and outbound connectivity after install

### Current Status
- Wazuh manager is installed
- Wazuh manager is enabled
- Wazuh manager is running
- TCP 1514 is listening
- The server remains reachable to external resources via NAT

### Notes
- The manager component is now installed and active on the Ubuntu server.
- Additional components such as the dashboard and indexer are separate and may be added later depending on the final lab design.
- The current lab state is sufficient to begin building monitored endpoint VMs.

## win-endpoint-01 Agent Installation

### Installation Summary
- Downloaded the Wazuh Windows agent inside the `win-endpoint-01` VM
- Installed the Wazuh Windows agent and configured it to use Wazuh manager IP `10.10.10.10`
- Verified that the `WazuhSvc` service exists and starts successfully

### Enrollment Verification
- Confirmed the Windows endpoint appeared on the Wazuh manager using `agent_control -l`
- Observed that the first enrollment used the default Windows hostname
- Renamed the endpoint to `win-endpoint-01`
- Confirmed a new agent entry appeared with the correct hostname
- Removed the stale `DESKTOP-S5M0R8U` agent entry after confirming the new endpoint entry was present

### Current Status
- `win-endpoint-01` is enrolled to the Wazuh manager
- The Windows agent is active
- The stale default-hostname entry has been removed

### Notes
- Because the Hyper-V VM did not have direct host-file access for the staged MSI, the effective agent installation used a guest-side download path.
- The Windows endpoint is now the first monitored agent enrolled into the Blue Lab Wazuh manager.

## linux-endpoint-01 Agent Installation

### Installation Summary
- Installed prerequisite packages required for repo-based Wazuh deployment
- Added the Wazuh repository and imported the signing key
- Installed the Wazuh Linux agent using deployment variables
- Configured the agent to use Wazuh manager IP `10.10.10.10`
- Configured the agent name as `linux-endpoint-01`
- Enabled and started the `wazuh-agent` service successfully

### Enrollment Verification
- Confirmed the Linux endpoint appeared on the Wazuh manager using `agent_control -l`

### Current Status
- `linux-endpoint-01` is enrolled to the Wazuh manager
- The Linux agent is active

### Notes
- The initial manual package-download approach was abandoned in favor of the official repo/deployment-variable method from Wazuh documentation.
- The Linux endpoint is the second monitored agent enrolled into the Blue Lab Wazuh manager.
