# Case 004: Registry Run Key Modification

## Case Summary
In this investigation, we examined a Sysmon registry modification event that captured a change to the Windows Run key.

Threat actors frequently abuse Run keys as a persistence mechanism to maintain access to compromised systems.

The goal of this investigation was to review the registry modification event, identify the process responsible for the change, and determine whether the activity was malicious or part of a controlled lab test.

-----

## Detection Source

### Log Source
- Microsoft-Windows-Sysmon/Operational

### Event Type
- Sysmon Event ID 13 - Registry Value Set

Sysmon Event ID 13 records when a registry value is created or modified. This telemetry provides visibility into registry persistence techniques commonly used by malware and attackers.

-----

## Key Evidence

### Process Executed
- powershell.exe

### Process Image
- C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

### Registry Path
- HKCU\Software\Microsoft\Windows\CurrentVersion\Run\LabStartupTest

### Registry Value
- notepad.exe

### User Context
- LABUSER

-----

## Analysis

The Windows Run registry key allows applications to automatically start when a user logs into the system.
Because this key directly controls startup behavior, it is frequently monitored by security teams and detection tools. Adversaries often modify Run keys to maintain persistence on compromised systems.
During this investigation, the registry value **LabStartupTest** was created and configured to launch **notepad.exe**.
Review of the Sysmon event confirmed that the registry modification was performed by **PowerShell**, which is commonly used for both legitimate administrative tasks and attacker activity.
Further analysis confirmed that this activity was intentionally generated within the cybersecurity monitoring lab environment to demonstrate how registry persistence techniques appear in Sysmon telemetry.

Indicators confirming the activity is benign:

- The registry change was manually executed during a controlled lab exercise
- The value launched a benign application (notepad.exe)
- No additional suspicious processes or network activity were observed

-----

## Outcome

The registry modification represents controlled testing activity within the cybersecurity monitoring lab. The event demonstrates how Sysmon captures registry Run key changes that could indicate persistence techniques used by attackers.

-----

## Skills Demonstrated

- Sysmon registry monitoring
- Registry persistence detection
- Analysis of Sysmon Event ID 13
- Windows startup persistence mechanisms
- Forensic artifact sanitization for public reporting

-----

## MITRE ATT&CK Reference

Technique  
T1547.001 — Boot or Logon Autostart Execution: Registry Run Keys

-----

## Evidence Artifact

[Registry Modification Event](../logs/case-004-registry-modification.xml)