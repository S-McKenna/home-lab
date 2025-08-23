# BitLocker Recovery Simulation Lab - VM Preparation

**Date:** June 30, 2025

This document details the preparation of a clean Windows 10 Pro virtual machine in VirtualBox for the BitLocker Recovery Simulation lab.

---

## 🎯 Objectives

- Create a clean Windows 10 Pro VM
- Enable TPM 2.0 for hardware-backed BitLocker encryption
- Use EFI firmware boot to simulate modern hardware
- Document all configuration steps prior to enabling BitLocker

---

## 🛠️ Environment

- **Host:** Windows 11 Pro
- **VirtualBox Version:** 7.1.6 r167084 (Qt6.5.3)
- **Oracle VM VirtualBox Extension Pack:** Installed
- **Guest OS:** Windows 10 Pro (22H2, x64)

---

## 🧩 VM Creation Process

### 1️⃣ Create New VM

- Name: `BitLocker-Client-TPM`
- Type: Microsoft Windows
- Version: Windows 10 (64-bit)
- Memory: 4096 MB
- CPUs: 2
- Disk: 50GB VDI (dynamically allocated)

---

### 2️⃣ Configure Storage

- **Controller:** SATA
- **Hard Disk:** `BitLocker-Client-TPM.vdi`
- **Optical Drive:** Attached Windows 10 22H2 ISO:
  ```
  Win10_22H2_English_x64v1.iso
  ```

---

### 3️⃣ Enable EFI and TPM

- **Settings > System > Motherboard:**
  - ✅ Enable EFI (Special OSes only)
  - ✅ TPM: Version 2.0

---

### 4️⃣ Start Installation (EFI Boot)

- Booted VM.
- Accessed EFI Boot Manager via `Esc` key.
- Selected:
  ```
  UEFI VBOX CD-ROM
  ```
- Pressed a key quickly when prompted:
  ```
  Press any key to boot from CD or DVD...
  ```
- Reached Windows Setup successfully.

---

### 5️⃣ Windows Installation

- Chose "I don't have a product key."
- Selected **Windows 10 Pro** edition.
- Custom installation on unallocated disk space (EFI GPT partitions created).

---

## 🟢 Next Steps

1. Complete Windows installation and initial setup.
2. Log in and verify TPM status:
   ```
   tpm.msc
   ```
   ✅ Expected result: "The TPM is ready for use."
3. Install Guest Additions for VirtualBox integration.
4. Take a clean snapshot:
   ```
   Snapshot Name: Clean Install with TPM
   ```
5. Proceed to BitLocker encryption and recovery simulation.

---

## ✨ Notes

- EFI firmware requires manually selecting the ISO from the Boot Manager when first booting.
- TPM 2.0 requires the Extension Pack installed before enabling.
- Fast keystroke tapping is needed at "Press any key to boot from CD/DVD..." prompt.

---
