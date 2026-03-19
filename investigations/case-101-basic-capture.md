# Case 101: ICMP Network Traffic Capture (Wireshark)

## Case Summary
In this investigation, we captured and analyzed network traffic using Wireshark to observe ICMP (ping) activity between a local host and an external system.

Packet capture analysis is a critical skill for security analysts, as it provides visibility into real-time network communications and helps identify both normal and suspicious behavior.

The goal of this investigation was to capture live network traffic, isolate ICMP packets, and analyze request and response patterns.

-----

## Detection Source

### Tool
- Wireshark

### Capture Type
- Live packet capture

Wireshark captures raw network packets and allows analysts to inspect protocols, communication patterns, and packet-level details.

-----

## Key Evidence

### Protocol Observed
- ICMP (Internet Control Message Protocol)

### Activity Type
- Echo Request / Echo Reply (Ping)

### Source IP
- Internal VM address (172.x.x.x range)

### Destination IP
- External public IP (104.x.x.x range)

### Packet Behavior
- Alternating request and reply traffic

-----

## Analysis

ICMP is commonly used for network diagnostics and connectivity testing. The "ping" command generates ICMP echo requests and receives echo replies from a destination system.

During this capture, the local system initiated ICMP echo requests to an external IP address. The destination responded with corresponding echo replies, confirming successful communication.

The packet sequence shows a consistent pattern:
- ICMP Echo Request sent from the local host
- ICMP Echo Reply received from the external system

This type of traffic is normal and expected during connectivity testing.

From a security perspective, ICMP traffic can also be used by attackers for:
- Network reconnaissance
- Host discovery
- Covert communication channels

In this scenario, the activity was intentionally generated in a controlled lab environment using the ping command to demonstrate how ICMP traffic appears in packet captures.

-----

## Outcome

The captured traffic represents normal ICMP communication between a host and an external system. The investigation confirms successful packet capture, filtering, and protocol analysis using Wireshark.

-----

## Skills Demonstrated

- Packet capture using Wireshark
- Protocol filtering (ICMP)
- Network traffic analysis
- Identification of request/response patterns
- Interpretation of packet-level data

-----

## MITRE ATT&CK Reference

Technique  
T1046 — Network Service Discovery

-----

## Evidence Artifact

- PCAP - [Wireshark Capture](../pcaps/case-101-basic-capture.pcapng)
- Readable [Packet Summary](../logs/case-101-basic-capture.txt)
