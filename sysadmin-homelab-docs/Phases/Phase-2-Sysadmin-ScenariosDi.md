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
- C:\Shares\IT IT-Users: Modify
- C:\Shares\HR HR-Users: Modify
- C:\Shares\Finance FIN-Users: Modify
- All subfolders retain SYSTEM Administrators, Creator Owner
![](Attatchments%20/Pasted%20image%2020260318145932.png)
#### Verification
- Accessed share as ituser01 from Windows 11 client via \\DC01\Shares 
- IT folder accessible, ituser01 has Modify via IT-Users group
- Test folder created
![](Attatchments%20/Pasted%20image%2020260318150719.png)
- HR and Finance folders denied access control working as expected
![](Attatchments%20/Pasted%20image%2020260318150742.png)

### User Lifecycle
#### Disabled Users
![](Attatchments%20/Pasted%20image%2020260401110659.png)
- Created Disabled Users OU via PowerShell
- Disabled Users OU serves as a staging area for offboarded accounts 
- Accounts moved here are disabled and stripped of group memberships but retained for audit and recovery purposes before permanent deletion
- Confirmed Via PowerShell and ADUC
#### Script: New-UserOnboard.ps1
##### Requirements
###### Inputs (prompted):
- First name
- Last name
- Department (menu: IT, HR, Finance)
- Password (initial, temporary)
###### Actions:
- Generate username (first initial + lastname, e.g. jsmith)
- Create AD user account with provided attributes
- Place user in correct OU based on department selection
- Add user to corresponding AD group (IT-Users, HR-Users, FIN-Users)
- Force password change at next logon
###### Output:
- Confirmation message showing username, OU, and group the user was added to

![](Attatchments%20/Pasted%20image%2020260401134509.png)
- Script written and saved to C:\Users\Administrator\Documents\New-UserOnboard.ps1

![](Attatchments%20/Pasted%20image%2020260401134110.png)

![](Attatchments%20/Pasted%20image%2020260401134155.png)

![](Attatchments%20/Pasted%20image%2020260401134424.png)
- Script successfully added user to Homelab, IT, and IT-Users Security group

![](Attatchments%20/Pasted%20image%2020260401133225.png)
![](Attatchments%20/Pasted%20image%2020260401135334.png)
- Testing for failure, password restriction, invalid department
- Tested successful user creation, password mismatch reprompt, invalid department reprompt, and password complexity enforcement

---

## Notes

---

## Troubleshooting

#### GPO-001 | Desktop Lockdown GPO linked to domain root
See issue log: [GPO-001](../Troubleshooting/Issues-Log.md)

![](Attatchments%20/Pasted%20image%2020260401104819.png)
Removed the incorrect domain link and linked the GPO to the Computers OU
![](Attatchments%20/Pasted%20image%2020260401105034.png)
![](Attatchments%20/Pasted%20image%2020260401105149.png)![](Attatchments%20/Pasted%20image%2020260401105215.png)