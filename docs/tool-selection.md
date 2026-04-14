# Tool Selection

## Phase 1 Monitoring Platform
The selected monitoring platform for Phase 1 is **Wazuh**.

## Why Wazuh Was Chosen
Wazuh was selected because it provides a practical entry point into security monitoring and detection engineering while remaining open source and realistic for a home lab. It supports endpoint monitoring for both Windows and Linux systems and can serve as the central platform for log collection, alerting, and basic investigation during the first phase of Blue Lab.

## What Wazuh Will Be Used For
- Collecting endpoint telemetry from Windows and Linux systems
- Reviewing logs and alerts in a central location
- Supporting basic security detections and monitoring workflows
- Building familiarity with agent-based monitoring and alert triage

## Why Other Tools Are Not Being Used Yet
Additional tools such as Suricata, Zeek, Velociraptor, TheHive, and SOAR platforms may be added in later phases. They are intentionally out of scope for Phase 1 so the project can begin with one stable monitoring platform and a manageable architecture.

## Supplemental Tools / Platforms
- Hyper-V for core Phase 1 virtualization
- VirtualBox for separate supplemental Kali Linux work outside the main Phase 1 lab design

## Phase 1 Principle
Phase 1 prioritizes simplicity, stability, and documentation over tool quantity.
