# Enterprise Security Assessment- Financial Services Environment 

For this project, as an external cybersecurity consultant, I was tasked with evaluating the network exposure, vulnerability posture, and security monitoring capabilities of a regional financial institution operating within a Windows/Linux enterprise environment.

The objective of this engagement was to:

- **Identify exposed services and network attack surfaces**

- **Conduct credentialed vulnerability scanning**

- **Analyze severity using CVSS and risk-based prioritization**

- **Evaluate logging and monitoring visibility**

- **Provide remediation guidance aligned with security best practices**

This assessment was conducted in an authorized simulated enterprise environment designed to mirror real-world financial sector infrastructure.

# 📍Phase 1 - Vulnerability Assessment 

<ins>**Network Enumeration (Nmap Findings)**</ins>

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

<ins>**Vulnerability Assessment (Nessus Findings)**</ins>

**Severity Breakdown**

- 🔴Critical: 4
- ⭕High: 10
- 🟠Medium: 19
- 🟡Low: 1

#### 🔴Critical Vulnerabilities 

***Apache Log4j(Multiple Variants)***

- Log4j < 2.16.0
- Log4j < 2.15.0 Remote Execution (RCE)
- Log4j 1.2 JMS Appender RCE
- Log4j 1.x Mutliple Vulnerabilities

![image](https://github.com/user-attachments/assets/60ab908b-cd86-46a5-ac60-508e6ad707dc)

#### ⭕High Vulnerabilities 
- Python Library Tornado 6.5.0 DoS
- OpenJDK 7 & 8 (Multiple Variants)
- ClamAV 1.0.0 <1.0.4
- ClamAV < 0.103.12
- Apache Log4j 1.2 JMSAppender Remote Code Execution

![image](https://github.com/user-attachments/assets/a37c9142-b883-4242-b412-cfe1da99a7ab)

![image](https://github.com/user-attachments/assets/2b9633eb-5c8e-4460-8a20-8a5d1e664174)



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



#### 🟡Low Vulnerabilities

- OpenJDK 8 <=8u402/11.0.0

![image](https://github.com/user-attachments/assets/e9920ece-78cd-497c-b9d8-9b9ea196b368)

