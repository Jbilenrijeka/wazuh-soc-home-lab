# Wazuh SOC Home Lab

A hands-on learning project focused on Windows security monitoring,
alert triage, and evidence-based investigation using Wazuh.

## Current Status

Planning and hardware assessment completed.
Wazuh installation and testing have not started.
The deployment configuration is still being evaluated.

## Project Goals

- Understand SIEM concepts and Wazuh architecture.
- Deploy Wazuh in a dedicated Linux virtual machine.
- Connect a Windows endpoint using the Wazuh agent.
- Collect and analyze Windows security events.
- Investigate alerts generated during controlled lab tests.
- Document evidence, findings, limitations, and lessons learned.

## Available Hardware

- Host operating system: Windows 11
- Processor: AMD Ryzen 7 4700U
- Installed RAM: 16 GB
- Hardware virtualization: enabled
- Free disk space at initial assessment: approximately 394 GB
- Virtualization platform: Oracle VirtualBox

Available RAM was approximately 4.6 GB during the initial assessment.
VM resource allocation and the Linux distribution have not been finalized.

## Planned Architecture

Windows endpoint with Wazuh agent
→ Linux VM running Wazuh server, indexer, and dashboard.

## Planned Documentation

- Architecture and installation notes
- Configuration and troubleshooting
- Controlled test scenarios
- Alert investigations and supporting evidence
- Lessons learned

## Lab Scope

Testing will be limited to owned or explicitly authorized systems.
Simulated activity will be clearly identified.
Only observed results will be reported.
Credentials and personal information will be removed before publication.
