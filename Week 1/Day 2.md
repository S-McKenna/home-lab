# 🖥️ 2: Create Domain Controller (DC-01)

**Date:** May 21, 2025
**Goal:** Create a VirtualBox VM running Windows Server 2022 to serve as the domain controller in the lab environment.

---
## ✅ Tasks Completed

### 1. Created the VM in VirtualBox
- Name: `DC-01`
- Memory: `4GB`
- CPU: `2 cores`
- HDD: `50GB (dynamically allocated, resized to 60GB later)`
- OS: `Windows Server 2022`
- Network: `NAT (may switch to internal network later)`
- ISO mounted: `Windows_Server_2022.iso`

📸 Screenshot: ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b19cca119e22a6792c63139b2084a336b8323b49/Week%201/screenshots/WinServer_2022_Install.png)

📸 Screenshot: 

![VirtualBox VM](https://github.com/S-McKenna/home-lab/blob/a40dc477947bbf37e22637f5585869efcd1058a9/Week%201/screenshots/Settings%20for%20WinServerDC.png)

---

### 2. Installed Windows Server 2022
- Booted from ISO
- Selected: **`Windows Server Standard (Desktop Experience)`**
- Set Administrator password
- Successfully logged into Windows

📸 Screenshots: ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b19cca119e22a6792c63139b2084a336b8323b49/Week%201/screenshots/InitialLogin.png)

📸 Screenshots:

![VirtualBox Vm](https://github.com/S-McKenna/home-lab/blob/a339f4b205938724f48e8ae4bb65d5b55c48f8b2/Week%201/screenshots/Logged%20IN.png)

---

### 3. Set Static IP
- IP Address: `192.168.10.10`
- Subnet Mask: `255.255.255.0`
- Gateway: `192.168.10.1`
- DNS: `left blank for now`

📸 Screenshot: ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b19cca119e22a6792c63139b2084a336b8323b49/Week%201/screenshots/StaticIPSettings_In_DC.png)

---

### 4. Renamed Computer
- Changed hostname to: `DC-01`
- Restarted to apply changes

📸 Screenshot: ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b19cca119e22a6792c63139b2084a336b8323b49/Week%201/screenshots/RenameDC.png)

### 5. Resized Virtual Disk
- Original size: `50GB`
- Used VBoxManage to increase to 60GB:
  Command:
  ```VBoxManage modifymedium disk "C:\Users\Samuel\VirtualBox VMs\DC-01\DC-01.vdi" --resize 61444```

- Issue: `"Extend Volume" option in Windows was greyed out`
- Resolution: `Installed MiniTool Partition Wizard Server Edition (Trial)`
- Successfully extended the C: partition to use unallocated space

------------------------------------------------------------
Notes and Lessons Learned

- VBoxManage commands are sensitive to syntax: "--resize" must not have a space.
- Windows built-in Disk Management can only extend into adjacent unallocated space.
- Recovery/system partitions can block C: from expanding.
- MiniTool Free doesn’t work on Windows Server — Server Edition (Trial) required.
- It’s useful to take screenshots and note CLI commands for lab documentation.

------------------------------------------------------------
Next Steps

- Promote DC-01 to a Domain Controller (install AD DS role)
- Set up DNS (and DHCP if desired)
- Create an internal VirtualBox network for domain lab isolation
