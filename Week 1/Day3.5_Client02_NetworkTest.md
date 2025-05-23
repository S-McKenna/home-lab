# 🧪 Day 3.5 – Client-02 Setup & Network Test

**Date Completed**: Friday, May 23, 2025  
**Estimated Time**: 1–1.5 hours  
**Status**: ✅ Complete  
**Objective**: Add second client VM and verify full VM network communication

---

## ✅ Tasks Completed

### 1. 🖥️ Created Client-02 VM
- Cloned from Client-01 to maintain consistency
- Renamed to `Client-02`
- Booted successfully and logged in

### 2. 🔧 Configured Network
- Verified all VMs (DC-01, Client-01, Client-02) are on the same **Host-only Adapter**
- Confirmed Adapter settings:
  - Adapter 1: Host-only Adapter (e.g., `VirtualBox Host-Only Ethernet Adapter`)

### 3. 🌐 Assigned Static IPs

| Device     | IP Address       | Subnet Mask     | Gateway        |
|------------|------------------|------------------|----------------|
| DC-01      | 192.168.10.10     | 255.255.255.0    | 192.168.10.1   |
| Client-01  | 192.168.10.20     | 255.255.255.0    | 192.168.10.1   |
| Client-02  | 192.168.10.30     | 255.255.255.0    | 192.168.10.1   |

- Configured via `Control Panel → Network Settings → IPv4 Properties`
- Verified using `ipconfig /all`

### 4. 📶 Confirmed Network Communication
- Used `ping` from each machine to the other two
- All devices responded successfully
- No packet loss
- Windows Defender Firewall disabled for testing

---

## 📸 Screenshots

Stored in:  
`/Screenshots/Day3.5_Client02_NetworkTest/`

Included:
- ✅ All 3 VMs running in VirtualBox or on desktop
- ✅ `ipconfig /all` for DC-01, Client-01, and Client-02
- ✅ Successful `ping` output from:
  - DC-01 ➜ Client-01 & Client-02
  - Client-01 ➜ DC-01 & Client-02
  - Client-02 ➜ DC-01 & Client-01

---

## 📝 Notes
- No network configuration issues encountered
- Reminder to re-enable Windows Defender Firewall after tests if needed
- Consider documenting NIC settings in a separate config log for traceability

---

**Next Step**:  
➡️ Promote DC-01 to a Domain Controller and begin Active Directory configuration in **Day 4**
