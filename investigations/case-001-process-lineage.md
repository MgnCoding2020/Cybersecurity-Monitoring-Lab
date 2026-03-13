# Case 001: Process Lineage Investigation

## Case Summary
In this investigation, I examined a Sysmon-captured process creation event showing the execution of git.exe from a PowerShell session.
The objective of this case is to demonstrate how Sysmon Event ID 1 can be used to identify process lineage and command executions within a Windows environment.

----
## Detection Source
### Log Source
Microsoft-Windows-Sysmon/Operational

### Event Type
Sysmon Event ID 1 - Process Creation

Sysmon Event ID 1 records detailed information about newly created processes, including the command executed, parent process, user context, and file hashes.

-----

## Key Evidence

### Process Executed
- git.exe
### Command Line
- "C:\Program Files\Git\cmd\git.exe" status
### Parent Process
- powershell.exe
### Integrity Level
- High
### User Context
- LAB\redacted-user
### Process Hashes
- MD5: 3806A1E58183FDBF9F70E0E4F2FDE61A
- SHA256: DA240FE9BC24895B3E04150A4990B8A6FF329ECABCD8F19684C2CC310DA5EF3F

----
## Process Lineage

Process lineage analysis is important because attackers often chain multiple processes together when executing commands or launching malicious tools.

Example of such:

```
winword.exe
└── powershell.exe
    └── cmd.exe
        └── malicious.exe
```
Understanding normal parent-child relationships can help analysts identify abnormal behavior during investigations.

----
## Analysis

This observation aligns with a typical developer workflow. The command **git status** was executed within a PowerShell session while working in a repository.

Several indicators help support that this activity is benign: 

- The process originated from an interactive PowerShell session.
- The executed command (git status) is a standard Git operation.
- The executable path points to the official Git for Windows installation directory.
- No suspicious command-line arguments or unusual parent processes were observed.

Monitoring process creation events is an important defensive capability because attackers frequently abuse CLI tools to execute scripts or launch payloads.

----
## Outcome
The event was determined to be legitimate. The activity was associated with development work inside the lab environment. No malicious behavior was observed. 

---
## Skills Demonstrated
- Sysmon log analysis
- Process creation monitoring
- Parent-child process relationship analysis
- CLI inspection
- Evidence sanitization for public sharing

## Evidence Artifact
[Process Lineage](logs/case-001-process-lineage.xml)
