# Enterprise Security Assessment- Financial Services Environment 

As an external cybersecurity consultant, I was hired to evaluate the network exposure, vulnerability posture, and monitoring capabilities of a regional financial institution: NextTech, operating within a Windows/Linux enterprise environment.

The objective of this engagement was to:

- **Identify exposed services and network attack surfaces**

- **Conduct credentialed vulnerability scanning**

- **Analyze vulnerabilities using CVSS risk scoring**

- **Evaluate security monitoring capabilities**

- **Provide risk-based remediation guidance**

This assessment was conducted within an authorized simulated enterprise environment designed to mirror real-world financial sector infrastructure.

# Table of Contents

- [Executive Summary](#executive-summary)
- [Assessment Methodology: Phase 1: Vulnerability Assessment](#assessment-methodology)
- **[Phase 1: Vulnerability Assessment](#phase-1-vulnerability-assessment)**
- [Risk Priorization](#risk-priorization)
- [Remediation Recommendations](#remediation-recommendations)
- **[Phase 2: Security Monitoring and Log Analysis](#phase-2-security-monitoring-and-log-analysis)**
- [Analysis Methodology](#analysis-methodology)
- [Key Findings](#key-findings)
- [Security Monitoring Observations](#security-monitoring-observations)
- [Recommendations](#recommendations)
- **[Phase 3: Incident Investigation and Indicators of Compromise (IoC) Analysis](#incident-investigation-and-indicators-of-compromise-analysis)**


# Executive Summary

A vulnerability assessment was conducted against the internal network `10.11.152.0/24` to evaluate the organization's security posture and identify exploitable weaknesses.

Network enumeration identified 2 active hosts, with one host exposing remote access services, including **SSH(TCP port 22)** and **RDP(TCP port 3389).**

Credentialed vulnerability scanning identified **127 vulnerabilities,** including: 

- 🔴4 Critical
- ⭕10 High
- 🟠19 Medium
- 🟡1 Low

The most severe findings included **Apache Log4j Remote Code Execution vulnerabilities**, outdated **OpenJDK installations**, and weak **SSL/TLS configurations.**

<ins>These vulnerabilities present a high risk of:</ins>

- Credential interception

- Remote code execution

- Lateral movement within the network

- Unauthorized system access

Immediate remediation was recommended for all **critical** and **high-severity vulnerabilities**, particularly those affecting publicly exposed services.

# Assessment Methodology

The assessment methodology followed guidance from:

- **NIST SP 800-15 - Technical Guide to Information Security Testing and Assessment**

Assessment phases included:

<ins>**Network Enumeration**</ins>

Identified live hosts and exposed services using: 

- **Nmap**

- **TCP SYN scanning**

- **Service version detection**


<ins>**Vulnerability Identification**</ins>

Credentialed vulnerability scanning performed using: 

- **Nessus Essentials**

Scans evaluated by: 

- **Known CVEs**

- **Patch levels**

- **Cryptographic weaknesses**

- **Weak configurations**


<ins>**Post-Assessment Analysis**</ins>

Findings were evaluated using: 

- **Risk prioritization**

- **CVSS severity scoring**

- **Mapping to NIST SP 800--53 control families**

**Tools Used:**

- Nmap
- Nessus Essentials
- Kali Linux

# 📍Phase 1: Vulnerability Assessment 

<ins>**Network Enumeration (Nmap Findings)**</ins>

**Target Subnet:** 10.11.152.1/24

**Hosts Identified:** 2
#

**Host 1: 10.11.152.61**
- All 1000 scanned ports marked as filtered or closed
- No externally exposed services detected
#

**Host 2: 10.11.152.165**
Two open ports identified: 

| Port | Service | Version 
| ---- | ------- | ------- 
| 22   |  SSH    | OpenSSH 9.9p1 Debian 3 (protocol 2.0)
| 3389 |  ms-wbt-server    | Microsoft Terminal Services

![image](https://github.com/user-attachments/assets/ab7f2d7d-3728-436d-9117-efe428d2214f)
#

**<ins>Attack Surface Analysis</ins>**

The presence of these exposed **remote access services** increases the organization's attack surface by introducing the following risks: 

- Brute-force credentialed attacks
- Remote exploitation of vulnerable services
- Lateral movement across systems
#

<ins>**Vulnerability Assessment (Nessus Findings)**</ins>

**Severity Breakdown**

| Severity | Count
| -------- | ------- 
| 🔴Critical   |  4 
| ⭕High |  10   
| 🟠Medium | 19
| 🟡Low | 1
| 🔵Info | 93

Total findings: **127 vulnerabilities**
#

#### 🔴Critical Vulnerabilities 

***Apache Log4j(Multiple Variants)***

- Log4j < 2.16.0
- Log4j < 2.15.0 Remote Execution (RCE)
- Log4j 1.2 JMS Appender RCE
- Log4j 1.x Mutliple Vulnerabilities

These vulnerabilities allow **remote code execution**, enabling attackers to execute arbitrary code on vulnerable systems.

![image](https://github.com/user-attachments/assets/60ab908b-cd86-46a5-ac60-508e6ad707dc)
#

#### ⭕High Vulnerabilities 
- Python Library Tornado 6.5.0 DoS
- OpenJDK 7 & 8 (Multiple Variants)
- ClamAV 1.0.0 <1.0.4
- ClamAV < 0.103.12
- Apache Log4j 1.2 JMSAppender Remote Code Execution

These vulnerabilities could enable: 

- Denial of service
- Privilege escalation
- Exploitation through outdated libraries

![image](https://github.com/user-attachments/assets/a37c9142-b883-4242-b412-cfe1da99a7ab)

![image](https://github.com/user-attachments/assets/2b9633eb-5c8e-4460-8a20-8a5d1e664174)
#



#### 🟠Medium Vulnerabilities

- Remote Desktop Protocol Server Man in the Middle Weakness
- SSL Certificate Cannot be Trusted
- Aqua Security Trivy < 0.51.2 Credential Leak
- ClamAV, 0.103.12 - System File Corruption
- SSL Anonymous Cipher Suites Supported
- Intel Media SDK Multiple Vulnerabilities (INTEL-SA-00935)
- OpenSSH < 10.0 DisableForwarding

![image](https://github.com/user-attachments/assets/619ade72-8651-42a6-8e71-24fd050faf76)
![image](https://github.com/user-attachments/assets/f79d18e8-f863-4fd1-b0c4-319a869b7d6c)
![image](https://github.com/user-attachments/assets/4e73d3e3-80e2-4a58-bda5-a84bbdb1864f)
![image](https://github.com/user-attachments/assets/9e943c6e-1ac0-4843-b309-68256a36db0c)

These weak configurations reduce overall system security and could assist attackers during lateral movement tactics.
#


#### 🟡Low Vulnerabilities

- OpenJDK 8 <=8u402/11.0.0

![image](https://github.com/user-attachments/assets/e9920ece-78cd-497c-b9d8-9b9ea196b368)

This outdated software can increase long-term risk if left unpatched.

# Risk Priorization
Based on CVSS severity, exposure surface, and exploit vulnerability, the following remediation priorities were identified: 

Immediate Remediation (Critical)

- Apache Log4j Remote Code Execution vulnerabilities
- All exposed RDP services without access management

High Priority

- Outdated OpenJDK installations
- Python Tornado DoS vulnerability

Medium Priority

- SSL certificate trust issues
- Anonymous cipher suites

# Remediation Recommendations
Key remediation actions include:

- Patch vulnerable Apache Log4j components immediately
- Upgrade Apache to version > 2.4.52
- Upgrade all outdated OpenJDK installations
- Restrict RDP access via VPN
- Harden SSH configurations
- Implement multi-factor authentication for all admin accounts
- Implement continuous monitoring via regular vulnerability assessments


# 📍Phase 2: Security Monitoring and Log Analysis

### Engagement Objective

Following the vulnerability assessment conducted in Phase 1, NextTech requested an evaluation of its security monitoring capabilities to determine whether the organization could detect malicious activity targeting its infrastructure.

The objective of this phase was to: 

- Assess the maturity of NextTech's **security monitoring and detection capabilities**
- Determine whether security logs could be **queried for threat indicators**
- Evaluate the organization's ability to **collect security monitoring data**
- Identify **potential indicators of compromise IoCs** in web server activity

Log data from multiple sources was analyzed to determine whether suspicious activity targeting the organization's web infrastructure could be identified.
#

### Log Sources Analyzed

Three log datasets representing web server activity were analyzed:

| Log Source | Description
| -------- | ------- 
| Access-1.log   |  HTTP access log containing web request activity 
| Apache_logs.log |  Apache web server activity logs   
| Access-2.log | Additional HTTP request logs used for anomaly analysis

These logs provided visibility into: 

- Client IP addresses
- HTTP methods
- Response Status Codes
- User Agent Strings
- Requested Resources
#

### Analysis Methodology 

Log analysis was conducted using standard command-line investigation techniques commonly used during incident response and threat hunting.

Because the environment lacked a centralized SIEM platform, log analysis relied on manual parsing and pattern detection.

**Tools Used:**

- Linux shell utilities
- Pattern matching techniques
- Manual review of suspicious entries

**<ins>Key commands used during analysis included:</ins>**

- `grep`
- `awk`
- `sort`
- `uniq`
- `wc`

These utilities allowed our analysts to efficiently query large log files and identify patterns associated with malicious activity.
#

### Key Findings

#### <ins>Access-1.log Analysis</ins>

The first dataset revealed several indicators associated with scanning activity and potential exploit attempts


| Indicator | Result
| -------- | ------- 
| GET Requests Logged  |  130 
| Unique HTTP Status Codes |  7  
| HTTP Tunneling Attempts (CONNECT)| 10
| Invalid Binary Request Lines |  60
| Unique User Agents |  55 
| Firefox Requests| 11

Several requests contained invalid request lines with raw binary data, which are often associated with

- vulnerability scanners
- automated reconnaissance tools
- TLS handshake attempts against non-TLS ports

##### ⚠️Exploitation Attempts Identified

Two requests attempting to exploit:

`CVE-2020-8515`

were detected in the log data. This vulnerability has historically been targeted in attacks against network devices and web services.
#

#### <ins>Apache Web Server Log Analysis</ins>
Analysis of the Apache web server logs revealed significant web traffic activity.


| Metric | Result
| -------- | ------- 
| Total Log Entries |  606 
| Unique Source IPs |  124  
| Most Active IP Address| 65.55.213.73
| Most Requested Resource |  /favicon.ico
| Successful HTTP Responses(200) | 526

The high number of successful HTTP responses indicates that the server is actively servicing requests from a wide range of external hosts.
#

#### <ins>Access-2.log Analysis</ins>
The final log dataset revealed additional activity related to potential reconnaissance and automated scanning.

| Indicator | Result
| -------- | ------- 
| GET Requests|  60
| Unique Source IP Addresses |  48  
| Successful Responses(200)| 19
| Client Errors(400) |  16

##### ⚠️First Connection Observed

The first request reaching the server originated from:

`104.245.97.236`

The high number of successful HTTP responses indicates that the server is actively servicing requests from a wide range of external hosts.

##### ⚠️Bot Activity Detected

Automated web crawler activity was identified.

| Bot       | Version       |
| --------- | ------------- |
| Googlebot | Googlebot/2.1 |

The presence of search engine bots demonstrates that the system is visible to automated internet crawlers.


##### ⚠️Shellshock Exploit Attempt

Log analysis also identified an attempted exploitation of the Shellshock vulnerability. 

Source IP:

`61.161.130.241`

Shellshock is a critical vulnerability that allows attackers to execute arbitrary commands on vulnerable systems via Bash.

##### ⚠️Browser Activity Observed

Analysis of user agent strings revealed the most frequently observed Firefox version:

`Firefox/31.0`

This browser version appeared **9 times** in the dataset.

##### ⚠️Most Common HTTP Method

The most frequently observed HTTP method was 

`GET`

with **60 total requests** recorded.
#

### Indicators of Suspicious Activity

Several indicators suggest that the system may be targeted by automated scanning tools and reconnaissance activity:

- Shellshock exploitation attempts
- HTTP tunneling attempts using CONNECT requests
- High number of requests from individual IP addresses
- Exploit attempts targeting CVE-2020-8515
- Malformed HTTP request lines containing binary data

These system patterns are consistent with attacker behavior observed during reconnaissance and vulnerability scanning.

### Security Monitoring Observations

The assessment revealed that NextTech is capable of collecting log data; however, it lacks the tooling required to actively monitor or provide alerts on suspicious activity. 

Limitations include:

- No automated alerting capability
- Manual log review required to detect threats
- Absence of centralized log aggregation

As a result of these limitations, potentially malicious activity may go undetected for extended periods of time.
#

### Recommendations

To improve detection capabilities, the following actions are recommended:

#### 🔑Deploy a SIEM Platform

A security information and event management(SIEM) platform would allow the organization to:

- Generate real-time security alerts
- Detect suspicious activity automatically
- Aggregate logs across systems

#### 🔑Strengthen Network Infrastructure

Firewall and intrusion detection/preventative rules should be implemented to block:

- Exploit payload signatures
- Known malicious IP addresses
- Repeated scanning attempts

#### 🔑Implement Automated Detection Rules

Detection rules should be created to identify: 

- Exploit attempts targeting known (CVEs - Common Vulnerabilities & Exposures)
- Malformed HTTP requests
- Repeated requests from single IP addresses
- Suspicious user agent patterns


# 📍Phase 3: Incident Investigation and Indicators of Compromise Analysis

### Engagement Objective

Following earlier findings of exposed services and suspicious log activity, NextTech reported multiple operational anomalies, including:

- Systems rebooting without authorization
- Files being renamed unexpectedly
- Sudden performance slowdowns

These events raised concerns that the organization may have experienced a security compromise.

The objective of this phase was to conduct a preliminary digital forensics investigation to determine whether indicators of compromise (IoCs) could be identified within the organization's IT infrastructure.

### Investigation Scope

The investigation focused on analyzing forensic artifacts provided by the organization.


| Artifact | Description
| -------- | ------- 
| `access-2.log`|  Web server access logs
| NextTechartifact.pcap |  Packet capture containing network traffic 

