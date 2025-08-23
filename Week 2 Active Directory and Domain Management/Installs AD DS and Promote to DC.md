# 🗂️ AD DS Install & Initial DNS Troubleshooting

## ✅ Completed Tasks

### 1. Install AD DS Role on DC-01
- Opened **Server Manager** on `DC-01`
- Installed **Active Directory Domain Services (AD DS)** via the Add Roles and Features wizard
- Confirmed installation completed successfully

### 2. Promote DC-01 to a Domain Controller
- Launched promotion wizard from Server Manager
- Chose **“Add a new forest”** with domain name: `lab.local`
- Set Directory Services Restore Mode (DSRM) password
- Left DNS selected (default)
- Accepted default NetBIOS name: `LAB`
- Completed prerequisites check and proceeded with install
- DC-01 rebooted and promotion confirmed successful

### 3. Verified Domain Controller Status
- Logged back in after reboot
- Confirmed domain presence in **Active Directory Users and Computers**
- Verified DNS Manager installed and `lab.local` visible under Forward Lookup Zones

---

## ❗Encountered Issue

While beginning DNS verification via `nslookup`, encountered an error:
> Default Server: UnKnown  
> Address: 192.168.10.10

- Attempted to resolve by updating network adapter’s preferred DNS to point to `192.168.10.10` via **Network and Sharing Center**
- Issue persists

---
## Update on Encountered Issue
1. Open DNS Manager  
2. Right-click Reverse Lookup Zones → New Zone...
3. In the Wizard:
   - Zone Type: Primary
   - Zone Name: 10.168.192.in-addr.arpa (for 192.168.10.0/24)
   - ✅ Allow secure dynamic updates
4. ✅ Result:  
   Reverse Lookup Zone created successfully.

---

## 🧪 Part 3: Testing Reverse DNS (PTR)

### 🔍 Initial Test Output (from DC-01):
```txt
nslookup 192.168.10.50
Server:  localhost.hsd1.ut.comcast.net
Address: ::1
*** localhost.hsd1.ut.comcast.net can't find 192.168.10.50: Non-existent domain
```

### ✅ Resolution Attempt:
- Updated both Ethernet adapters to use 192.168.10.10 as DNS
- Still received resolution failure

### 🔧 Forced Query to Internal DNS:
```txt
nslookup 192.168.10.50 192.168.10.10
Server:  DC-01.lab.local
Address: 192.168.10.10
*** DC-01.lab.local can't find 192.168.10.50: Non-existent domain
```

### ✅ Root Cause:
No PTR record was present in reverse zone

---

## 🛠️ Part 4: Manual PTR Record Creation

1. Open DNS Manager
2. Navigate to:
   DC-01 > Reverse Lookup Zones > 10.168.192.in-addr.arpa
3. Right-click zone → New Pointer (PTR)...
4. Enter:
   - IP last octet: 50
   - Host: web01.lab.local
5. Click OK

---

## 🧪 Final Verification

### ✅ Successful nslookup:
```txt
nslookup 192.168.10.50 192.168.10.10
Server:  DC-01.lab.local
Address: 192.168.10.10

Name:    web01.lab.local
Address: 192.168.10.50
```

---

## 🧩 Notes
- Creating the reverse zone after the A record prevented automatic PTR creation
- Manually creating the PTR resolves the issue
- Reverse DNS is now operational within lab.local
---

## 🛠️ Next Steps (Planned)

### Part 2 – Step 2: Install DHCP Role
- Open **Server Manager > Add Roles and Features**
- Add **DHCP Server** role
- Complete DHCP post-install configuration (authorize server)

### Part 2 – Step 3: Configure DHCP Scope
- Open DHCP Management Console
- Create new IPv4 Scope:
  - **Name**: `LabScope`
  - **Start IP**: 192.168.10.20
  - **End IP**: 192.168.10.100
  - **Subnet Mask**: 255.255.255.0
  - **Default Gateway**: 192.168.10.1
  - **DNS Server**: 192.168.10.10
- Activate the scope

### Part 2 – Step 4: Confirm DHCP Functionality
- Boot Client VM(s) to check for IP lease
- Verify assigned IP is in scope range
- Refresh DHCP console > Address Leases

### DNS Troubleshooting Follow-Up
- Continue working on resolving `nslookup` "UnKnown" server issue
- Verify:
  - DC-01 has a valid forward lookup zone for `lab.local`
  - Proper reverse lookup zone is optionally configured
  - Firewall isn't blocking DNS
  - `127.0.0.1` and/or `192.168.10.10` are correctly set as DNS

---

## 📸 Suggested Screenshots

- AD DS install wizard summary page 
  ![VirtualBox AD DS Install ](https://github.com/S-McKenna/home-lab/blob/3d8b3157e81dd97e55238290d49012647274c048/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/AD%20DS%20Install.png)
- Domain setup screen (`lab.local`) 
  ![VirtualBox Domain Screen](https://github.com/S-McKenna/home-lab/blob/3d8b3157e81dd97e55238290d49012647274c048/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/New%20Forest%20Name%20Lab%20Local.png)
- Final confirmation screen before promotion (pending upload)
- DNS Manager showing Forward Lookup Zones (pending upload)

