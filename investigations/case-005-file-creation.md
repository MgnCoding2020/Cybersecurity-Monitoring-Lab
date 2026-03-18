# Case 005: File Creation in Temp Directory

## Case Summary
In this investigation, we examined a Sysmon file creation event that captured PowerShell creating an executable file in the user's temporary directory.

File creation events in temporary directories are commonly monitored by security teams because attackers often stage payloads, tools, or malware in writable locations before execution.

The goal of this investigation was to review the file creation event, identify the process responsible for creating the file, and determine whether the activity was malicious or part of a controlled lab test.

-----

## Detection Source

### Log Source
- Microsoft-Windows-Sysmon/Operational

### Event Type
- Sysmon Event ID 11 - File Create

Sysmon Event ID 11 records file creation activity and can provide useful visibility into suspicious file drops, staged payloads, and malware written to disk.

-----

## Key Evidence

### Process Executed
- powershell.exe

### Process Image
- C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

### Target Filename
- C:\Users\*\AppData\Local\Temp\lab-payload.exe

### Rule Name
- EXE

### User Context
- LABUSER

-----

## Analysis

Temporary directories are commonly monitored during investigations because they are writable by standard users and frequently abused by attackers for payload staging.

In this case, PowerShell created a file named **lab-payload.exe** in the local temporary directory. A filename ending in **.exe** can appear suspicious because attackers often write executable files to disk before launching them.

This type of activity can be associated with malware staging, tool transfer, or payload delivery in real-world environments.

Further analysis confirmed that this activity was intentionally generated in the cybersecurity monitoring lab to demonstrate how file creation activity appears in Sysmon telemetry.

Indicators confirming the activity is benign:

- The file was manually created during a controlled lab exercise
- The file was empty and not executed
- No additional suspicious child processes were observed
- No malicious network activity was associated with the event

-----

## Outcome

The file creation event represents controlled testing activity within the cybersecurity monitoring lab. The event demonstrates how Sysmon captures the creation of potentially suspicious files in a temporary directory.

-----

## Skills Demonstrated

- Sysmon file creation monitoring
- Analysis of Sysmon Event ID 11
- File path and process attribution
- Investigation of suspicious file staging behavior
- Forensic artifact sanitization for public reporting

-----

## MITRE ATT&CK Reference

Technique  
T1105 — Ingress Tool Transfer

-----

## Evidence Artifact

[File Creation Event](../logs/case-005-file-creation.xml)