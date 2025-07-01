# BitLocker Lab - Windows 10 VM with VirtualBox TPM

## Overview
This lab demonstrates configuring BitLocker Drive Encryption on a Windows 10 Pro VM running in VirtualBox with TPM emulation enabled. It covers:

- Verifying Windows activation
- Setting up BitLocker with TPM
- Resolving TPM validation issues
- Encrypting the OS drive
- Preparing for recovery scenarios

---

## Environment Details
- **Hypervisor:** VirtualBox
- **Guest OS:** Windows 10 Pro
- **TPM:** VirtualBox TPM Emulation
- **Encryption Mode:** New encryption mode (XTS-AES)

---

## Steps Performed

### 1. Verify Windows Activation
**Action:**  
Checked activation status.

**Result:**  
Windows was **not activated** (Error 0xC004F213).  
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Windows%20not%20activated.png)

---

### 2. Launch BitLocker Drive Encryption
**Action:**  
Opened **Manage BitLocker** and confirmed C: drive status as **BitLocker Off**.  
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Before%20BitLocker%20Encryption.png)

---

### 3. Start BitLocker Wizard
**Action:**  
Clicked **Turn on BitLocker**.

**Observation:**  
Wizard initially skipped unlock method selection, going directly to recovery key backup.

---

### 4. Backup Recovery Key
**Action:**  
Manually wrote down the recovery key (saving to C: was not allowed).

---

### 5. Select Encryption Settings
- **How much to encrypt:** Entire drive
- **Encryption mode:** New encryption mode
- **System check:** Initially enabled

---

### 6. Reboot and Error Handling
**Action:**  
Rebooted for system check.

**Result:**  
Error:
```
BitLocker could not be enabled.
The data drive specified is not set to automatically unlock...
C: was not encrypted.
```
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Snag.png)

---

### 7. Verify TPM Status
**Action:**  
Opened `tpm.msc`.

**Result:**  
TPM status confirmed: **Ready for use.**
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/TPM%20Status.png)

---

### 8. Configure Group Policy
**Action:**  
Enabled Group Policy to allow BitLocker without compatible TPM:
- **Policy:** Require additional authentication at startup
- **Setting:** Enabled
- **Allow BitLocker without a compatible TPM:** Checked
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Updated%20GP%20policy.png)

---

### 9. Restart BitLocker Wizard
**Action:**  
Reran the wizard.

**Unlock Method:**  
Selected **Let BitLocker automatically unlock my drive.**
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Choose%20unlock.png)

---

### 10. Backup New Recovery Key
**Action:**  
Recorded the new recovery key.

---

### 11. Encryption Started
**Action:**  
Launched encryption without system check.
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/BitLocker%20Encrypting.png)

---

### 12. Encryption Completed
**Result:**  
Encryption completed successfully.
![VirtualBoxBitLocker](https://github.com/S-McKenna/home-lab/blob/b84d06df97ef472bb2d692edc64a24952556c8c4/screenshots/BitLocker/Encryption%20Complete.png)

---

## Next Steps
- Simulate BitLocker recovery prompt.
- Test unlocking with recovery key.
- Practice suspending and disabling BitLocker.

---

## Notes
- VirtualBox TPM emulation does not fully support Secure Boot or PCR binding.
- Group Policy overrides are needed to allow auto-unlock.
