# 🖥️ Home Lab: DHCP & Domain Join (`Client-01`)

## ✅ Objective
Configure `Client-01` to use DHCP from `DC-01` and join the `lab.local` Active Directory domain.

---

## 🧱 Environment Overview

| Machine    | IP Assignment | Role               | Network Adapter         |
|------------|---------------|--------------------|--------------------------|
| DC-01      | Static         | Domain Controller, DHCP, DNS | Internal Network: `intnet` |
| Client-01  | DHCP           | Domain-Joined Client | Internal Network: `intnet` (NAT disabled during setup) |

---

## 🔌 Step 1: Network Adapter Configuration

### VirtualBox Settings:
- **Adapter 1**: Internal Network (`intnet`)
- **Adapter 2**: NAT (disabled for both VMs during domain setup)

---

## 🌐 Step 2: Enable DHCP on Client-01

1. Open **Control Panel > Network and Sharing Center**
2. Go to **Change adapter settings**
3. Right-click Ethernet > **Properties**
4. Double-click **Internet Protocol Version 4 (TCP/IPv4)**
5. Select:
   - ✅ Obtain an IP address automatically
   - ✅ Obtain DNS server address automatically
6. Click OK > Close

📸 Screenshot: IPv4 properties window with DHCP enabled
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/DHCP%20Auto%20Client%2001.png)

---

## 🔁 Step 3: Verify DHCP Lease

1. Open **Command Prompt**
2. Run:
   ```bash
   ipconfig /release
   ipconfig /renew
   ipconfig /all
   ```
3. Confirm:
   - DHCP Enabled: Yes
   - IP Address: From `192.168.10.100–200`
   - DNS Server: `192.168.10.10`
   - DNS Suffix: `lab.local`

📸 Screenshot: `ipconfig /all` showing DHCP settings
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/DHCP%20Client%2001%20in%20Scope.png)

---

## 🔎 Step 4: Test DNS

Run the following:
```bash
ping dc-01.lab.local
nslookup dc-01.lab.local
```

📸 Screenshot: Successful name resolution of `dc-01.lab.local`
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/DHCP%20Ping%20and%20NSLookup%20from%20Client%2001.png)

---

## 🏢 Step 5: Join the Domain

1. Right-click **This PC > Properties**
2. Click **Advanced system settings > Computer Name > Change**
3. Select **Domain**, enter: `lab.local`
4. Use credentials:
   - Username: `LAB\Administrator` *or* `Administrator@lab.local`
5. Accept the welcome prompt and restart

📸 Screenshot: Domain join prompt and success message
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/Joined%20Lab%20Local.png)

---

## 🔐 Step 6: Log In as Domain User

1. After restart, click **Other user**
2. Enter:
   - Username: `lab\\Administrator`
   - Password: Domain password

📸 Screenshot: Login screen with domain account
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/Logging%20in%20as%20Administrator%20Client%2001%20to%20lab%20local.png)

---

## 🧾 Step 7: Verify Domain Membership

1. Right-click **This PC > Properties**
2. Click **Advanced system settings**
3. Under **Computer Name** tab, confirm:
   ```
   Member of: lab.local
   ```

📸 Screenshot: System Properties window showing domain membership
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/17c7dbddb8002e6f87965a8eae06e73450dd2664/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%204/Member%20of%20Lab%20local.png)

---

## ✅ Outcome

- `Client-01` successfully received a DHCP lease from `DC-01`
- DNS resolution confirmed functional
- Domain join completed
- Login with domain account verified

---

## 🔜 Next Steps (Optional)

- Create a standard domain user to test user policies
- Begin exploring Group Policy Objects (GPO)
- Configure shared folders or set up a File Server role

