# Case 002: Encoded PowerShell Execution

## Case Summary
In this investigation, we examined a Sysmon process creation event that captured the execution of PowerShell using the `-EncodedCommand` argument.
Encoded PowerShell commands are commonly used by attackers to obfuscate scripts and avoid detection.
The goal was to analyze the command execution, decode the payload, and determine whether the activity was malicious or benign.

-----

## Detection Source
### Log Source
- Microsoft-Windows-Sysmon/Operational
### Event type
- Sysmon Event ID 1 - Process Creation

Sysmon Event ID 1 records detailed telemetry for process creation events, including command-line arguments, user context, process lineage, and executable hashes.

----

## Key Evidence
### Process Executed
- powershell.exe
### Command Line
- powershell.exe -EncodedCommand VwByAGkAdABlAC0ASABvAHMAdAAgACIASABlAGwAbABvACAARABGAEkAUgAgAEwAYQBiACIA
### Parent Process
- powershell.exe
### Integrity Level
- High
### User Context
- Lab\redacted-user
### Process Hashes
- MD5: 2E5A8590CF6848968FC23DE3FA1E25F1
- SHA256: 9785001B0DCF755EDDB8AF294A373C0B87B2498660F724E76C4D53F9C217C7A3

----

## Process Lineage
```
powershell.exe
└── powershell.exe -EncodedCommand
```
This indicates that an existing PowerShell session spawned a second PowerShell process with an encoded command argument.

Process chaining like this is commonly seen during automated scripts or attacker activity where PowerShell is used as an execution engine.

----

## Encoded Payload Analysis
The CLI argument contains a Base64-encoded PowerShell command:
```VwByAGkAdABlAC0ASABvAHMAdAAgACIASABlAGwAbABvACAARABGAEkAUgAgAEwAYQBiACIA```

After decoding, the command resolved to: 

``` Write-Host "Hello DFIR Lab"```

This command simply outputs a message to the PowerShell console and does not perform harmful activity.

-----

## Analysis

These PowerShell-encoded commands are frequently associated with malicious activity because they allow the threat actor to hide scripts from basic inspection.

Some common attacker use cases include:
- Executing obfuscated payload
- Downloading remote malware
- Bypassing CLI logging visibility
- Executing malicious scripts through phishing documents

In this analysis, the encoded payload was intentionally generated in the lab environment to demonstrate how it appears in Sysmon logs.

Indicators confirming the activity is benign: 
- The decoded command performs a simple console output
- The execution occurred in a controlled lab environment
- The parent process was an interactive PowerShell session
- No suspicious network activity or additional payload execution occurred

-----

## Outcome
The event represents a controlled testing activity performed within the cybersecurity monitoring lab environment. No malicious behavior was observed.

----

## Skills Demonstrated
- Sysmon process creation analysis
- Detection of encoded PowerShell execution
- Base64 payload decoding
- Command-line argument inspection
- Process lineage analysis
- Forensic artifact sanitization for public reporting

------
## Evidence Artifact

[Encoded PowerShell](../logs/case-002-encoded-powershell.xml)

-----
