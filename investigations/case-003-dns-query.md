# Case 003: DNS Query Activity

----

## Case Summary
This investigation examines a Sysmon process creation event that captured the execution of the ```nslookup``` utility used to perform a DNS query for the domain ```github.com```.
DNS activity is monitored during incident investigations because malicious activity frequently relies on DNS to locate command-and-control servers, download payloads, or perform data exfiltration.

The objective of this case was to analyze the execution of the DNS lookup command and understand how DNS activity appears in Sysmon telemetry. 

-----

## Detection Source
### Log Source
- Microsoft-Windows-Sysmon/Operational
### Event Type
- Sysmon Event ID 1 - Process Creation

Sysmon can log DNS query events directly (Event ID 22), this case focused on the execution of the ```nslookup``` command used to initiate the query.

----

## Key Evidence
### Process Executed
- nslookup.exe
### Command Line
- "C:\Windows\system32\nslookup.exe" github.com
### Parent Process
- powershell.exe
### Integrity Level
- High
### User Context
- LAB\redacted-user
### Process Hashes
- MD5: F2E3950C1023ACF80765C918791999C0
- SHA256: 55AB032D256ADBE3FDE40CF90FE83BA5EAB591E04AD720161ED8E6EF059CA747

----
## Process Lineage
```
powershell.exe
└── nslookup.exe github.com
```

This indicates that the DNS query was executed from an interactive PowerShell session.

Understanding process lineage helps analysts determine whether activity was initiated by a user, automated script, or potentially malicious software.

----
## DNS Activity Analysis
Command executed:
``` nslookup github.com```

The ```nslookup``` utility is a standard Windows diagnostic tool used to query DNS servers and resolve domain names into IP addresses.

In enterprise environments, DNS activity is closely monitored  because attackers often rely on DNS for: 
- Locating command-and-control infrastructure
- Downloading malware payloads
- Data exfiltration using DNS tunneling
- Domain generation algorithms (DGA)

In this investigation, the query targeted the well-known domain github.com, which is commonly used for legitimate software development and code hosting.

------
## Analysis
Indicators confirm the behavior is benign:
- The command was executed from an interactive PowerShell session.
- The queried domain (github.com) is a legitimate and widely used service.
- The activity occurred within the controlled cybersecurity monitoring lab environment.
- No additional suspicious processes or commands were spawned following the lookup.

While this activity is normal in this case, similar DNS queries could indicate malicious behavior in other contexts.
DNS is often investigated to identify suspicious or newly registered domains associated with malware campaigns.

---
## Outcome
The event represents legitimate DNS lookup activity performed during lab testing. No malicious indicators were identified.

This case demonstrates how command-line DNS utilities appear within Sysmon process creation logs and how analysts can interpret such activity during investigations.

---
## Skills Demonstrated
- Sysmon process creation analysis
- Command-line monitoring
- DNS investigation fundamentals
- Process lineage interpretation
- Forensic artifact documentation
- Safe log sanitization for public sharing

----
## Evidence Artifact
[DNS Query](logs/case-003-dns-query.xml)

---