# Wazuh Installation

## wazuh-server

### Repository Setup
- Imported the Wazuh GPG signing key
- Added the Wazuh APT repository for the 4.x release line
- Updated package lists successfully

### Installation
- Initial attempt to install package `wazuh` failed because the package was not found
- Confirmed that the correct package for the manager component is `wazuh-manager`
- Installed `wazuh-manager` on Ubuntu Server 24.04 LTS

### Service Verification
- Enabled the `wazuh-manager` service
- Started the `wazuh-manager` service
- Verified service status with `systemctl status wazuh-manager`
- Checked for expected listener activity using `ss`

### Current Status
- Wazuh manager is installed
- Wazuh manager is enabled
- Wazuh manager is running

### Notes
- The manager component is now installed and active on the Ubuntu server
- Additional components such as the dashboard and indexer are separate and may be added later depending on the final lab design
