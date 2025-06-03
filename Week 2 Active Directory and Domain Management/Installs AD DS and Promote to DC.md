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

- AD DS install wizard summary page (pending upload)
- Domain setup screen (`lab.local`) (pending upload)
- Final confirmation screen before promotion (pending upload)
- DNS Manager showing Forward Lookup Zones (pending upload)

