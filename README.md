# Wazuh SOC Home Lab

A hands-on learning project focused on Windows security monitoring,
alert triage, and evidence-based investigation using Wazuh.

## Current Status

- Deployed the Wazuh manager, indexer, and dashboard in a Linux virtual machine and connected a Windows 11 endpoint.
- Reviewed an agent-stop alert (Wazuh rule `506`) and documented the findings and limitations.
- Validated Windows Security event collection and Wazuh detection on 6 November 2026 through a controlled failed-logon test. Windows recorded two Event ID `4625` events, and Wazuh displayed two matching alerts under rule `60122`. See the [Windows Failed Logon Investigation](docs/failed-logon-investigation.md).
- Updated AnyIO on the Windows endpoint and reviewed the corresponding Wazuh resolution events. See the [AnyIO Vulnerability Remediation](docs/anyio-vulnerability-remediation.md) report.

## Project Goals

- Understand SIEM concepts and Wazuh architecture.
- Deploy Wazuh in a dedicated Linux virtual machine.
- Connect a Windows endpoint using the Wazuh agent.
- Collect and analyze Windows security events.
- Investigate alerts generated during controlled lab tests.
- Document evidence, findings, limitations, and lessons learned.

## Available Hardware

- Host operating system: Windows 11 Pro
- Processor: AMD Ryzen 7 4700U
- Installed RAM: 16 GB
- Hardware virtualization: enabled
- Free disk space at initial assessment: approximately 394 GB
- Virtualization platform: Oracle VirtualBox

Available RAM was approximately 4.6 GB during the initial assessment.
These figures describe the initial assessment, not current resource usage.
Final VM resource allocation and Linux distribution details are not
documented in this README yet.

## Architecture

The Windows 11 host runs the Wazuh agent and hosts the Linux virtual
machine through VirtualBox.

The Windows agent communicates with the Wazuh manager inside the Linux VM.
The VM also runs the Wazuh indexer and dashboard.

- Windows endpoint: ASUSwin11
- Agent ID: 001
- Agent version shown in the dashboard: 4.14.9
- Agent status at the time of capture: active

## Deployment Evidence

### Wazuh Installation

The installation output reports completion of the Wazuh indexer,
manager, and dashboard installation, ending with "Installation finished."

![Wazuh installation output](<Screenshot 2026-11-02 192752.png>)

### Windows Agent Connection

The endpoint overview shows ASUSwin11 (ID 001) running Windows 11 Pro
with an active agent status at the time of capture.

This confirms the observed connection status. It does not by itself
verify collection of every Windows event channel.

![Windows agent shown as active](<Screenshot 2026-11-02 174044.png>)

## First Alert Review — Wazuh Agent Stopped

### Objective

Identify the affected endpoint, inspect the alert fields, and distinguish
confirmed observations from assumptions.

### Observations

| Field | Observed value |
| --- | --- |
| Dashboard timestamp | 2 November 2026, 17:37:29.249 |
| Agent name | ASUSwin11 |
| Agent ID | 001 |
| Rule ID | 506 |
| Rule level | 3 |
| Description | Wazuh agent stopped. |
| Manager name | wazuhlab |
| Location | wazuh-remoted |

The alert contains the following full log message:

    ossec: Agent stopped: 'ASUSwin11->any'.

The timestamp above is retained as displayed in the dashboard.

### Events View

The Events table shows the alert, affected agent, timestamp,
rule level, and rule ID.

![Agent-stopped alert in the Events table](<Screenshot 2026-11-02 192716.png>)

### Alert Details

The Document Details view shows the underlying alert fields and full log.

![Rule 506 alert details](<Screenshot 2026-11-02 192658.png>)

### Assessment

Wazuh recorded an agent-stop event for ASUSwin11.
A separate endpoint screenshot shows the agent as active at 17:40
on the same date, after the displayed alert time.

The cause of the stop was not established.
The available evidence does not establish malicious activity or
endpoint compromise.

The alert includes MITRE ATT&CK mapping T1562.001,
"Disable or Modify Tools." This mapping provides investigation context;
it does not prove that an attacker disabled the agent.

### Limitations

- The cause of the agent stop remains unknown.
- This event was not documented as a controlled agent-stop test.
- The screenshots do not establish the exact duration of any monitoring gap.
- Active agent status does not prove that Windows Security events
  are being collected and generating alerts.

## Lessons Learned

- Agent connectivity and event collection require separate verification.
- Windows Event IDs and Wazuh rule IDs identify different things.
- An alert or MITRE ATT&CK mapping alone does not prove an attack.
- Investigation notes should distinguish evidence, interpretations,
  and unresolved questions.

## Next Steps

- Document the Linux distribution and VM resource allocation.
- Expand installation and troubleshooting notes.

## Planned Documentation

- Architecture and installation notes
- Configuration and troubleshooting
- Controlled test scenarios
- Alert investigations and supporting evidence
- Lessons learned

## Lab Scope

Testing is limited to owned or explicitly authorized systems.
Simulated activity will be clearly identified.
Only observed results will be reported.
Credentials and unnecessary personal information must be removed
from evidence before publication.
