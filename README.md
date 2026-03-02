# Enterprise Security Assessment- Financial Services Environment 

For this project, as an external cybersecurity consultant, I was tasked with evaluating the network exposure, vulnerability posture, and security monitoring capabilities of a regional financial institution operating within a Windows/Linux enterprise environment.

The objective of this engagement was to:

- **Identify exposed services and network attack surfaces**

- **Conduct credentialed vulnerability scanning**

- **Analyze severity using CVSS and risk-based prioritization**

- **Evaluate logging and monitoring visibility**

- **Provide remediation guidance aligned with security best practices**

This assessment was conducted in an authorized simulated enterprise environment designed to mirror real-world financial sector infrastructure.

# Phase 1 - Vulnerability Assessment 

**Network Enumeration (Nmap Findings)**

**Target Subnet:** 10.11.152.1/24

**Hosts Identified:** 2


**Host 1: 10.11.152.61**
- All 1000 scanned ports marked as filtered or closed
- No externally exposed services detected

**Host 2: 10.11.152.165**
Two open ports identified: 

| Port | Service | Version 
| ---- | ------- | ------- 
| 22   |  SSH    | OpenSSH 9.9p1 Debian 3 (protocol 2.0)
| 3389 |  ms-wbt-server    | Microsoft Terminal Services
