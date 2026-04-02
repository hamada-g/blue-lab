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

### Notes
- Current Wazuh documentation installs the manager as `wazuh-manager`, not `wazuh`
- Additional components such as Filebeat, Wazuh indexer, and Wazuh dashboard are separate and will be addressed later
