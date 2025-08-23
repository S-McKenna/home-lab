# 🛠️ DHCP Role Setup on DC-01 (`lab.local`)

## 🧱 Objective
Install and configure the **DHCP Server** role on `DC-01` to provide dynamic IPs and network settings to lab clients.

---

## 🔧 Step-by-Step Instructions (with Screenshots)

### 1. Install the DHCP Role

1. Open **Server Manager**
2. Click **Manage > Add Roles and Features**
3. In the wizard:
   - Select **Role-based or feature-based installation**
   - Choose **DC-01** as the destination server
   - Under **Server Roles**, check **DHCP Server**
   - Click through the prompts and click **Install**

📸 **Screenshot #1**: "Select Server Roles" screen with *DHCP Server* checked  
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Server%20Roles%20selection.png)
📸 **Screenshot #2**: "Confirmation" screen before clicking **Install**
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Confirmation%20before%20install.png)

---

### 2. Post-Install Configuration Wizard

1. After install completes, click **Complete DHCP configuration**
2. The **DHCP Post-Install Wizard** will launch
3. Click **Next**, then **Use current credentials** or specify a domain admin account
4. Click **Commit** to authorize the DHCP server in AD

📸 **Screenshot #3**: DHCP Authorization step  
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Authorization%20Step.png)
📸 **Screenshot #4**: "Summary" screen after successful post-config
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Summary%20Done%20Screen.png)

---

### 3. Open DHCP Management Console

1. From Server Manager, go to **Tools > DHCP**
2. Expand your server > **IPv4**

📸 **Screenshot #5**: DHCP Console with your server and IPv4 node visible
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Console%20with%20Server%20and%20IPv4%20node.png)

---

### 4. Create a New DHCP Scope

1. Right-click **IPv4 > New Scope**
2. Scope Wizard:
   - **Name:** Lab Scope
   - **Start IP:** 192.168.10.100
   - **End IP:** 192.168.10.200
   - **Subnet Mask:** 255.255.255.0

📸 **Screenshot #6**: "Scope Name" entry  
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20DNS%20Configuration.png)

3. Click **Next** through the Exclusions and Delay screen
4. Set **Lease Duration** as desired
5. At **Configure DHCP Options**, select: **Yes, I want to configure these options now**

---

### 5. Configure DHCP Options

#### 🚪 Router (Default Gateway)
- Enter: `192.168.10.1` *(or leave blank)*
- Click **Add** > **Next**

📸 **Screenshot #7**: Router screen with 192.168.10.1 entered
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Router%20Scope.png)

#### 🌐 Domain Name and DNS Servers
- **Parent Domain:** lab.local
- **DNS Server IP:** 192.168.10.10
- Click **Add** > **Next**

📸 **Screenshot #8**: DNS configuration with lab.local and 192.168.10.10
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20DNS%20Configuration.png)

#### 📮 WINS Servers
- Leave blank > **Next**

📸 **Screenshot #9**: WINS Server screen (blank)
![VirtualBox](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20WINS%20Blank.png)

#### 🏁 Activate Scope
- Select: **Yes, I want to activate this scope now**
- Click **Next** > **Finish**

📸 **Screenshot #10**: Final confirmation screen showing scope activation
![VirtualBox DHCP](https://github.com/S-McKenna/home-lab/blob/5df8367ae32e932e730905a7b2a4f54003d023da/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/DHCP%20Scope%20Active.png)

---

## ✅ Next Step
Test DHCP by launching a second VM (`Client-01`), enable DHCP on its network adapter, and confirm IP lease in the correct range.
