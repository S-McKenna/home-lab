# Active Directory: Users, Groups, and Profile Management

**Date Completed:** June 24, 2025  
**Domain Name:** `lab.local`  
**Host:** `DC-01` (Domain Controller)

---

## 🗂️ Step 1: Organizational Unit (OU) Structure

Created the following Organizational Units to logically separate users and computers:

- `IT`
- `HR`
- `Support`
- `Workstations`

> ⚠️ **Note from experience:** After each OU is created, be sure to reselect `lab.local` before creating the next one. Otherwise, the new OU may accidentally nest inside the previously selected OU.  
> If an OU was created in the wrong location and is protected from deletion, enable **View > Advanced Features**, then go to the **Object** tab in the OU's properties and uncheck "Protect object from accidental deletion" before deleting.

📸 **Screenshots:**
- OU structure shown in ADUC left-hand tree
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/New%20OUs%20added.png)

---

## 👤 Step 2: User Accounts

Created three users, each placed into their appropriate department OU:

| Username | Full Name     | OU       |
|----------|---------------|----------|
| jdoe     | John Doe      | IT       |
| asmith   | Alice Smith   | HR       |
| btaylor  | Ben Taylor    | Support  |
| mwilliamson | Mark Williamson | Support |

📸 **Screenshots:**
- Summary screen before clicking Finish
- OU folder showing the user object
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/New%20User%20Created%20in%20Support%20OU.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/IT%20Users.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/HR%20Users.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/Support%20Users.png)

---

## 👥 Step 3: Security Groups

Created security groups for departmental access and assigned users to them:

| Group Name    | Scope   | Type      | Members   |
|---------------|---------|-----------|-----------|
| IT_Admins     | Global  | Security  | jdoe      |
| HR_Users      | Global  | Security  | asmith    |
| Support_Staff | Global  | Security  | btaylor   |

📸 **Screenshots:**
- Group creation screen (before clicking OK)
- Members tab showing user assignments
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/IT_Admins%20Group%20Creation.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/HR_Users%20Group%20Creation.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/Support_Staff%20Group%20Creation.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/IT_Admins%20Member%20List.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/HR_Users%20Member%20List.png)
![VirtualBoxScreenshot](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/Support_Staff%20Members%20List.png)

---

## 💼 Step 4: Profile Tab – Home Folder and Logon Script

Configured the following on the **Profile tab** for user `jdoe`:

- **Home Folder:** Mapped `H:` drive to `\\dc-01\Users\jdoe`
- **Logon Script:** `logon.bat`

**Script Location:**

```
C:\Windows\SYSVOL\sysvol\lab.local\scripts\logon.bat
```

**Logon.bat contents:**
```bat
@echo off
echo Welcome %USERNAME%!
```

### Shared Folder Setup (`\\dc-01\Users`):
- Created local folder `C:\Users` (or another location)
- Shared with **Authenticated Users** with Change + Read permissions
- NTFS permissions set for Modify access

📸 **Screenshots:**
- Profile tab for `jdoe` showing Home Folder and Logon Script fields
- `logon.bat` in the scripts folder
![VirtualBoxScreenshots](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/jdoe%20homefolder.png)
![VirtualBoxScreenshots](https://github.com/S-McKenna/home-lab/blob/2d2081fa31cb93f71fd664378e611b6dfc83efe8/Week%202%20Active%20Directory%20and%20Domain%20Management/screenshots/June%2024/jdoe%20logon%20scipt%20enabled.png)

---

## ✅ Summary

This week covered:
- OU creation and structure design
- User and group creation with scoped organization
- Profile configuration (Home folders and logon scripts)

---

## 🔜 Next Steps (Preview)

- Begin working with Group Policy Objects (GPOs)
- Apply user-based or computer-based settings via GPO
- Test policy propagation using `gpupdate` and `rsop.msc`
- Configure restricted access to user home folders (ACLs)
