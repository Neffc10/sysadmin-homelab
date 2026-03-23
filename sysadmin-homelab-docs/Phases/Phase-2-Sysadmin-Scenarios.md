# Phase 2 -- [Sysadmin Scenarios]
## Contents
- [Goal](#goal)
- [Deliverables](#deliverables)
- [Build Log](#build-log)
- [Notes & Observations](#notes--observations)
- [Troubleshooting](#troubleshooting)
## Goal
Simulate real-world IT administration tasks performed in a managed domain environment.

## Deliverables
- Group Policies configured and enforced (password policy, desktop restrictions, software control)
- File shares created with NTFS permissions mapped to AD groups
- User lifecycle workflows documented (onboarding, password reset, offboarding)
- Common helpdesk scenarios simulated and documented (locked accounts, mapped drives, profile issues)
- Ubuntu Server VM basic Linux administration performed

---

## Build Log

### Group Policy Objects

#### Password Policy GPO
- Scope: homelab.local (domain-wide)
- Purpose: Enforce minimum password standards across all domain accounts

![](Attatchments%20/Pasted%20image%2020260318131756.png)
##### Settings
- Minimum password length: 10 characters
- Maximum password age: 90 days
- Minimum password age: 1 day
- Password must meet complexity requirements: Enabled
- Enforce password history: 10 passwords remembered
- Store passwords using reversible encryption: Disabled

#### Desktop Lockdown GPO
- Scope: Homelab OU (applies to all department users)
- Purpose: Restrict standard users from accessing system settings 
  and command prompt
![](Attatchments%20/Pasted%20image%2020260318134411.png)
##### Settings
- Prohibit access to Control Panel and PC Settings: Enabled
- Prevent access to the command prompt: Enabled

### File Shares

#### Share Configuration
- Share name: Shares
- Path: C:\Shares
- Server: DC01

#### Share Permissions (C:\Shares)
- Administrators: Full Control
- Domain Users: Change
![](Attatchments%20/Pasted%20image%2020260318142359.png)
#### NTFS Permissions (C:\Shares root)
- SYSTEM: Full Control
- Administrators: Full Control
- Domain Users: Read & Execute
- Creator Owner: Full Control
![](Attatchments%20/Pasted%20image%2020260318144707.png)
#### NTFS Permissions (Subfolders)
- C:\Shares\IT — IT-Users: Modify
- C:\Shares\HR — HR-Users: Modify
- C:\Shares\Finance — FIN-Users: Modify
- All subfolders retain SYSTEM, Administrators, Creator Owner
![](Attatchments%20/Pasted%20image%2020260318145932.png)
#### Verification
- Accessed share as ituser01 from Windows 11 client via \\DC01\Shares 
- IT folder accessible — ituser01 has Modify via IT-Users group
- Test folder created
![](Attatchments%20/Pasted%20image%2020260318150719.png)
- HR and Finance folders denied — access control working as expected
![](Attatchments%20/Pasted%20image%2020260318150742.png)

---

## Notes
[Anything learned, gotchas, or worth remembering from this phase.]

---

## Troubleshooting
[Link to any relevant issues log entries.]