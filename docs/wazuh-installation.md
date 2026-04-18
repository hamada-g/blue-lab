# Wazuh Installation

## wazuh-server

### Deployment Scope
Blue Lab Phase 1 currently uses the **Wazuh manager** component on `wazuh-server`.

### Notes
- This Phase 1 baseline does not include the Wazuh dashboard or indexer.
- The current deployment is sufficient for manager service validation, agent enrollment, telemetry verification, and monitored endpoint development.

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
- The manager component is installed and active on the Ubuntu server.
- The present lab state is sufficient to support monitored endpoint enrollment in Phase 1.

### Event Visibility / Validation Notes
- During Phase 2A monitoring validation, raw event visibility was enabled on the manager to support endpoint telemetry troubleshooting and analysis.
- The Wazuh manager was configured to retain archive data so collected events could be reviewed even when they did not generate a higher-level alert.
- Review of `archives.json` confirmed that Windows Event Channel data from `win-endpoint-01` was reaching the manager.
- Initial archive validation showed that manager-side activity from `wazuh-server` itself could dominate terminal output during testing, which made raw archive review more useful than alert-only review for early telemetry validation.
- Readability improved significantly when manager inspection was performed over SSH from the Windows host rather than through the limited Hyper-V console window.
- `jq` was added on `wazuh-server` to make JSON archive output readable during telemetry validation and troubleshooting.

### Preferred Validation Workflow
- SSH into `wazuh-server` from the Windows host rather than using the small Hyper-V console window
- Use manager-side archive review to inspect raw collected events from monitored endpoints
- Use `jq` to filter and format archive output for readability
- Use targeted test events that clearly create new processes or channel-specific activity when validating Windows telemetry

### Example Validation Commands
```bash
sudo /var/ossec/bin/agent_control -l
sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | tail -n 10 | jq '{timestamp, agent: .agent.name, location, decoder: .decoder.name, rule: (.rule.description // "no rule"), full_log}'
sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | grep -a '"location":"EventChannel"' | tail -n 10 | jq '{timestamp, agent: .agent.name, location, decoder: .decoder.name, rule: (.rule.description // "no rule"), full_log}'
sudo grep -a '"name":"win-endpoint-01"' /var/ossec/logs/archives/archives.json | jq 'select(.location=="EventChannel") | .full_log |= fromjson | select(.full_log.win.system.eventID=="4688" or (.full_log.win.system.providerName | test("PowerShell"))) | {timestamp, agent: .agent.name, eventID: .full_log.win.system.eventID, provider: .full_log.win.system.providerName, channel: .full_log.win.system.channel, message: .full_log.win.system.message}'

---

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
- Removed the stale default-hostname agent entry after confirming the corrected endpoint entry was present

### Current Status
- `win-endpoint-01` is enrolled to the Wazuh manager
- The Windows agent is active
- The stale default-hostname entry has been removed

### Notes
- Because the Hyper-V VM did not have direct host-file access for the staged MSI, the effective agent installation used a guest-side download path.
- The Windows endpoint is the first monitored agent enrolled into the Blue Lab Wazuh manager.

---

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
- The initial manual package-download approach was abandoned in favor of the official repo-based deployment method from Wazuh documentation.
- The Linux endpoint is the second monitored agent enrolled into the Blue Lab Wazuh manager.
