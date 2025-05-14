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
*Writeup in progress. More to come.*
