# SOC-webstrike-pcap-analysis
# WebStrike Incident Response Lab  
## Web Shell Exploitation & Data Exfiltration Analysis

## Overview

This project presents a full Security Operations Center (SOC) investigation of a simulated web application compromise involving:

- Malicious file upload exploitation
- Web shell deployment
- Command-and-Control (C2) establishment
- Unauthorized data exfiltration

The investigation was performed through packet capture (PCAP) analysis to identify the attacker’s methods, indicators of compromise, and remediation actions.

---

## Project Objective

To investigate a simulated cyber attack by:

- Identifying the compromise vector
- Tracing attacker activity
- Detecting command execution behavior
- Analyzing exfiltration attempts
- Recommending mitigation controls

---

## Skills Demonstrated

- Incident Response
- PCAP Analysis
- Threat Hunting
- Network Traffic Investigation
- Web Application Security Analysis
- IOC Identification
- Security Reporting
- Vulnerability Assessment

---

## Tools Used

- Wireshark
- Kali Linux
- HTTP Traffic Analysis
- Packet Inspection Techniques

---

## Attack Scenario

A vulnerable web application file upload function was exploited to upload a malicious PHP web shell using a double-extension bypass.

The attacker successfully:

1. Uploaded malicious payload
2. Executed remote commands
3. Established outbound communication
4. Attempted sensitive file exfiltration

---

## Key Findings

### 1. Initial Compromise

**Attack Vector:** File Upload Vulnerability

**Payload Uploaded:**  
`image.jpg.php`

### Why It Worked

The application validated only the outer extension (`.jpg`) while the server interpreted the inner extension (`.php`) as executable code.

---

### 2. Vulnerable Location

`/reviews/uploads/`

#### Security Weaknesses Identified

- Inadequate file validation
- No MIME-type verification
- Executable upload directory
- Lack of upload sanitization

---

### 3. Command & Control Activity

**Outbound Port:** `8080`

The attacker established a reverse shell connection for remote command execution.

---

### 4. Threat Attribution Indicators

**User-Agent:**
`Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0`

**Geolocation:** Tianjin, China

---

### 5. Exfiltration Attempt

**Targeted File:**  
`/etc/passwd`

### Security Impact

Potential exposure of:

- System user accounts
- Privilege mapping information
- Internal enumeration data

---

## Indicators of Compromise (IOCs)

| Indicator | Value |
|----------|------|
| Malicious File | image.jpg.php |
| Port | 8080 |
| Upload Path | /reviews/uploads/ |
| Target File | /etc/passwd |

---

## MITRE ATT&CK Mapping

| Tactic | Technique |
|-------|-----------|
| Initial Access | Exploit Public-Facing Application |
| Execution | Command Shell |
| Persistence | Web Shell |
| Command & Control | Application Layer Protocol |
| Collection | Data from Local System |
| Exfiltration | Exfiltration Over Web Channel |

---

## Remediation Recommendations

### Application Security

- Enforce strict file type validation
- Validate file signatures (magic bytes)
- Rename uploaded files server-side
- Disable script execution in upload directories

### Network Security

- Monitor outbound traffic
- Block unauthorized port 8080 traffic
- Implement egress filtering

### Detection Engineering

- Alert on suspicious upload patterns
- Monitor abnormal HTTP POST requests
- Detect dual-extension uploads

---

## Lessons Learned

This lab demonstrates how weak upload validation can lead to full remote code execution and data compromise.

Key takeaway:

**Never trust file extensions alone.**

---

## Author

Cybersecurity Analyst Portfolio Project

Focus Areas:
- SOC Analysis
- Incident Response
- Threat Detection
- Vulnerability Assessment
