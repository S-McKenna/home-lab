# Day 4 – Internal Lab Networking Setup (May 24, 2025)

This document summarizes the configuration of internal networking for the home lab environment using VirtualBox. The goal was to establish dual-adapter networking for each VM, enabling internal communication and internet access.

---

## 🖧 Network Topology

Each VM was configured with two network adapters:
- **Adapter 1:** Internal Network (`intnet`) for local lab communication
- **Adapter 2:** NAT for outbound internet access

| Device     | IP Address     | Subnet Mask       | Gateway        | DNS Server      |
|------------|----------------|-------------------|----------------|-----------------|
| DC-01      | 192.168.10.10  | 255.255.255.0     | 192.168.10.1   | (self)          |
| Client-01  | 192.168.10.20  | 255.255.255.0     | 192.168.10.1   | 192.168.10.10   |
| Client-02  | 192.168.10.30  | 255.255.255.0     | 192.168.10.1   | 192.168.10.10   |

---

## 🔧 Configuration Summary

### ✅ VirtualBox Adapter Settings (for each VM)
- **Adapter 1**
  - Attached to: `Internal Network`
  - Name: `intnet`
  - Adapter Type: `Intel PRO/1000 MT Desktop (82540EM)`
  - Promiscuous Mode: `Deny`
- **Adapter 2**
  - Attached to: `NAT`
  - Adapter Type: `Intel PRO/1000 MT Desktop (82540EM)`
  - Promiscuous Mode: `Deny`

### ✅ Static IPs (Configured in Guest OS)
- Each VM's internal adapter was assigned a static IP as per the table above.
- Gateway is set for logical structure; NAT provides external routing.

### ✅ DNS Preparation
- Clients were configured to use `192.168.10.10` (DC-01) as their preferred DNS server in preparation for Active Directory setup.

---

## 🖼 Screenshots Captured

- [x] VirtualBox Adapter settings (each VM)
![Adapter Settings](https://github.com/S-McKenna/home-lab/blob/fc2e3fb01e314afe10ae4b0ef345e4b2e3f0c86e/Week%201/screenshots/Client%2001%20Both%20Adapters.png)
![Adapter Settings](https://github.com/S-McKenna/home-lab/blob/fc2e3fb01e314afe10ae4b0ef345e4b2e3f0c86e/Week%201/screenshots/Client%2002%20Both%20Adapters.png)
    
- [x] DNS settings showing `192.168.10.10` on Client VMs
![DNS on Client VMS](https://github.com/S-McKenna/home-lab/blob/fc2e3fb01e314afe10ae4b0ef345e4b2e3f0c86e/Week%201/screenshots/DNS%20points%20to%20DC01.png)
![DNS on Client VMS](https://github.com/S-McKenna/home-lab/blob/fc2e3fb01e314afe10ae4b0ef345e4b2e3f0c86e/Week%201/screenshots/Client%2002%20DNS%20points%20to%20DC01.png)
    
- [x] Network diagram included (see below)

![Network Diagram](https://github.com/S-McKenna/home-lab/blob/fc2e3fb01e314afe10ae4b0ef345e4b2e3f0c86e/Week%201/screenshots/Network%20Diag%20May%2024%202025.png)

---

## 📝 Notes

- Internet connectivity confirmed via NAT adapter.
- Internal connectivity confirmed via previous ping tests (omitted from screenshot documentation).
- Network setup is now ready for DNS and Active Directory domain services.

---

*Generated on May 24, 2025 as part of the Home Lab Build.*


---

## ▶️ Next Steps (Completed: TBD)

**Estimated Time:** 1 hour

### Tasks:
- [ ] Boot all 3 virtual machines (DC-01, Client-01, Client-02)
- [ ] Run ping tests again between all machines to verify network persistence
- [ ] Create a GitHub repository: `home-labs_IT-support-env`
- [ ] Upload Week 1 documentation and screenshots

### Upload Checklist:
- [ ] First screenshots from Week 1 (IP configs, adapter settings, etc.)
- [ ] `README.md` draft summarizing Week 1's progress

### 📸 Screenshots to Capture:
- [ ] All 3 machines logged in (visible desktops or terminals)

This will wrap up the foundational network layer and transition into directory services and lab automation workflows.

---
