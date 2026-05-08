**Metasploitable 2: Full-Spectrum Penetration Testing Lab**

**Project Overview**
This repository contains a detailed technical breakdown of a series of security audits conducted on the Metasploitable 2 vulnerable Linux virtual machine. This project demonstrates the systematic approach of a penetration test, including environment baseline verification, active reconnaissance, vulnerability research, exploitation, and post-exploitation credential auditing.


**🛠️ Technical Stack**
Host OS: Windows 10/11

Virtualization: Oracle VirtualBox

Attacker: Kali Linux 2024.x

Target: Metasploitable 2 (Linux 2.6.24)

Networking: Host-Only Adapter (Isolated Network)


** Lab Modules & Technical Execution**
**1. Tool Baseline & Local Auditing**
Before engaging the target, I performed a baseline audit of the Nmap tool suite using the loopback interface. This ensured that the scanning engine was correctly interpreting open/closed states without network latency interference.

SYN Stealth Scan (-sS): Verified the top 1,000 common ports on localhost.

Full Range Audit (-p-): Audited all 65,535 TCP ports to confirm a secure local baseline.



**2. Network Reconnaissance (Phase I)**
Using Nmap, I mapped the attack surface of the target machine (192.168.56.101).

Key Findings: Identified several critical legacy services, specifically FTP (21), SSH (22), and Telnet (23).

Service Fingerprinting: Detected vsftpd 2.3.4 and OpenSSH 4.7p1.



**3. Vulnerability Exploitation (Phase II)**
I targeted the vsftpd 2.3.4 service based on its known history of a "backdoor" vulnerability where a specific sequence of characters in the username triggers a listener on port 6200.

Exploitation Tool: Metasploit Framework (msfconsole).

Module: exploit/unix/ftp/vsftpd_234_backdoor.

Result: Successful remote command execution as the root user. This provided total administrative control over the target system.



**4. Credential Auditing & Hash Cracking (Phase III)**
Post-exploitation, I focused on auditing the system's authentication security. I extracted the /etc/shadow file to obtain password hashes.

Cracking Engine: John the Ripper.

Success Rate: 75% of targeted accounts were cracked using a standard wordlist and incremental brute-force.

Plaintext Recovery: * msfadmin:msfadmin (Weak/Default Credential)

klog:123456789 (Weak Numeric Sequence)

sys:batman (Dictionary Word)
