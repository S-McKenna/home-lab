# 🏗️ Windows Home Lab - Day 1 Setup

## 📁 Folder Setup
Created base folders for organizing lab resources:
```
C:\Users\samue\OneDrive\Desktop\Home Lab
C:\Users\samue\OneDrive\Desktop\Home Lab\ISO Files
```

---

## 💽 ISO Downloads
Downloaded the following operating systems from official sources:
- ✅ `SERVER_EVAL_x64FRE_en-us.iso` (Windows Server 2022 Evaluation)
- ✅ `Win10_22H2_English_x64.iso` (Windows 10 22H2)

Saved both ISOs to:
```
C:\Users\samue\OneDrive\Desktop\Home Lab\ISO Files
```

---

## 🧰 VirtualBox Setup
Had previously installed **VirtualBox 7.x** and today created two virtual machines:

### 🖥️ WinServer2022-DC
- Base Memory: 4096 MB
- CPUs: 2
- Virtual Hard Disk: 50 GB (dynamically allocated)
- Mounted ISO: `SERVER_EVAL_x64FRE_en-us.iso`

### 🖥️ Win10Client01
- Base Memory: 4096 MB
- CPUs: 2
- Virtual Hard Disk: 50 GB (dynamically allocated)
- Mounted ISO: `Win10_22H2_English_x64.iso`
- Windows 10 successfully installed

---

## 🛠️ Current Status
- ✅ Folder structure and ISO downloads complete
- ✅ VirtualBox installed
- ✅ Two VMs created
- ✅ Windows 10 installation finished
- ⏳ Windows Server installation pending

---

## 📸 Screenshots 
Place images in `/screenshots/` and reference them below:

- Folder structure
- ISOs saved in `C:\Users\samue\OneDrive\Desktop\Home Lab\ISO Files`
- ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b94f3c7e9718e8a3ee7d893c3dcf248652dc5964/screenshots/Server%202022%20ISO%20Download%20Screenshot.png)
- VirtualBox main screen with both VMs
- ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/7de62051794ea9ca7dd97ce9f53a52d2c3b69c0d/screenshots/Virtual%20Box%20with%20all%20VMs.png)
- VM settings for each machine
- Windows 10 post-install login screen
- ![VirtualBox VM List](https://github.com/S-McKenna/home-lab/blob/b94f3c7e9718e8a3ee7d893c3dcf248652dc5964/screenshots/WIN10%20Installed%20on%20Virtual%20Box.png)

---

## 🧭 Next Steps
1. Install Windows Server 2022 on `WinServer2022-DC`
2. Promote to Domain Controller (install AD DS)
3. Configure DNS & DHCP
4. Join `Win10Client01` to domain
5. Snapshot base configs
6. Begin group policy testing
