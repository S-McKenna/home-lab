# BitLocker Recovery Simulation Lab - Windows 10 VM with VirtualBox TPM

## Overview
This lab demonstrates forcing a BitLocker recovery scenario and restoring TPM auto-unlock after successful recovery.

---

## Environment Details
- **Hypervisor:** VirtualBox
- **Guest OS:** Windows 10 Pro
- **TPM:** VirtualBox TPM Emulation
- **Encryption Status:** Fully encrypted OS drive

---

## Steps Performed

### 1. Force BitLocker Recovery
**Command Used:**
```
manage-bde -forcerecovery C:
```

**Result:**
- Recovery was enforced on next boot.
- Numerical Password (recovery key) became the required unlock method.
![VirtualBoxBitLockerRecovery](https://github.com/S-McKenna/home-lab/blob/91ff7b50040093a56361ee50c5ddb7a0b640daa3/screenshots/BitLocker/BrokenBitlocker/Bitlocker-recovery-prompt.png)

---

### 2. Reboot and Enter Recovery Key
**Action:**
- Restarted the VM.
- At BitLocker Recovery screen, manually entered the 48-digit recovery key.

**Result:**
- Windows booted normally into the desktop.
![VirtualBoxBitLockerRecovery](https://github.com/S-McKenna/home-lab/blob/91ff7b50040093a56361ee50c5ddb7a0b640daa3/screenshots/BitLocker/BrokenBitlocker/Bitlocker-recovery-prompt-2.png)

---

### 3. Check Protector Status
**Command Used:**
```
manage-bde -status C:
```

**Result:**
- Key Protectors showed:
  ```
  Numerical Password
  ```
![VirtualBoxBitLockerRecovery](https://github.com/S-McKenna/home-lab/blob/91ff7b50040093a56361ee50c5ddb7a0b640daa3/screenshots/BitLocker/BrokenBitlocker/Numerical%20Password.png)
---

### 4. Restore TPM Auto-Unlock
**Commands Used:**

**Add TPM Protector:**
```
manage-bde -protectors -add C: -tpm
```

**Remove Numerical Password Protector:**
```
manage-bde -protectors -delete C: -type RecoveryPassword
```

**Result:**
- TPM protector restored as the sole key protector.
- Auto-unlock functionality reinstated.

**Verification:**
```
manage-bde -status C:
```
> Output:
```
Key Protectors:
    TPM
```
![VirtualBoxBitLockerRecovery](https://github.com/S-McKenna/home-lab/blob/91ff7b50040093a56361ee50c5ddb7a0b640daa3/screenshots/BitLocker/BrokenBitlocker/TPM%20Protector.png)
---

## Notes
- Forcing recovery is a valuable practice scenario to ensure you can unlock systems securely.
- After recovery, confirm which key protectors are active to avoid repeated recovery prompts.

---
