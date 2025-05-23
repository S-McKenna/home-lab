## 🔧 Troubleshooting: Forgotten Administrator Password

**Issue:** Forgot the local Administrator password after initial setup of the Windows Server 2022 VM (`DC-01`).

### 🛠 Resolution Steps

1. **Booted into Windows Server 2022 ISO** and selected:
   - `“Repair your computer” > “Troubleshoot” > “Command Prompt”`

2. **Located correct Windows partition** by testing drive letters:
   - Found `Windows\System32` folder on `D:` (not `C:` as expected in recovery mode)

3. **Swapped utilman.exe with cmd.exe** using:
   ```cmd
   d:
   cd \windows\system32
   ren utilman.exe utilman.bak
   copy cmd.exe utilman.exe
   ```

4. **Rebooted the VM**, then clicked the **Ease of Access icon** at the login screen to open an elevated command prompt.

5. **Reset the password** with:
   ```cmd
   net user Administrator NottheactualP@ssw0rd!
   ```

6. **Logged into Windows successfully**

---

### 🧼 Post-Recovery Cleanup

Once logged in, restored `utilman.exe`:

```cmd
cd C:\Windows\System32
takeown /f utilman.bak
icacls utilman.bak /grant administrators:F
del utilman.exe
ren utilman.bak utilman.exe
icacls utilman.exe /setowner "NT SERVICE\TrustedInstaller"
```

---

### 🧠 Lessons Learned

- Recovery mode may map system drives to different letters (e.g., D: instead of C:)
- System32 files are protected by TrustedInstaller; ownership must be temporarily changed to modify
- Always snapshot or write down critical credentials during lab setup
- This recovery method is useful for locked-out local admin accounts
