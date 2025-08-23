# Day 3: Initial Communication Test – DC-01 and Client VM

**Date**: `Thursday, May 22, 2025  `

**Goal**: `Confirm internal network communication between Domain Controller (DC-01) and Windows Client (Win10Client01) via ICMP (ping) after assigning static IPs and configuring VirtualBox networking.`

---

## ✅ VM Configuration Summary

### DC-01 (Windows Server 2022)
- **Name**: `WInServer-DC`
- **RAM**: 4GB
- **CPU**: 2 cores
- **HDD**: 60GB
- **IP Address**: `192.168.10.10`
- **Network Adapter**:  
  - Type: `Intel PRO/1000 MT Desktop`  
  - Attached to: `Internal Network`  
  - Network Name: `intnet`  
- **Firewall**: Disabled (Domain, Private, Public)

### Client (Windows 10)
- **Name**: Win10Client01
- **RAM**: 4GB
- **CPU**: 2 cores
- **HDD**: 50GB
- **IP Address**: `192.168.10.20`
- **Network Adapter**:  
  - Type: `Intel PRO/1000 MT Desktop`  
  - Attached to: `Internal Network`  
  - Network Name: `intnet`  
- **Firewall**: Disabled (Domain, Private, Public)

---

## 🔧 Tasks Completed

1. Verified static IP configurations on both VMs using `ipconfig /all`
2. Switched both VM network adapters to **Internal Network** (named `intnet`)
3. Rebooted both VMs to apply changes
4. Performed ping test:
   - `Client ➜ Server` (ping 192.168.10.10) ✔️
   - `Server ➜ Client` (ping 192.168.10.20) ✔️

---

## 📸 Screenshots

- `Screenshots/Client-Ping-Test` – Successful ping from Client to Server  ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/55c1adb573aca01342f4c0b9b6e29ebdc7ad46e8/Week%201/screenshots/Successful%20Ping%20Test%20between%20Client%20and%20Server.png)
- `Screenshots/VM-Network-Settings Client` – Client:  ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/55c1adb573aca01342f4c0b9b6e29ebdc7ad46e8/Week%201/screenshots/Client%20Adapter.png)
- `Screenshots/VM-Network-Settings Server` – Server:  ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/55c1adb573aca01342f4c0b9b6e29ebdc7ad46e8/Week%201/screenshots/Server%20Adapter.png)

---

## 📝 Notes

- Initial issue with NAT adapter prevented inter-VM communication. Resolved by switching to **Internal Network**.
- **Next Step** (optional): Add a second network adapter (NAT) to each VM to provide internet access while maintaining internal lab connectivity.
