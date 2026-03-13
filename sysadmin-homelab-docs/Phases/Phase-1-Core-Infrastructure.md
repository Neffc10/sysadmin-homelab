# Phase 1 — Core Infrastructure
## **Goal:** Deploy and configure the core virtual infrastructure including a Windows domain environment and Linux server.

## **Deliverables:**
- Windows Server 2022 VM deployed and configured
- Server promoted to Domain Controller
- Active Directory, DNS, and DHCP operational
- Windows 11 client VM deployed and domain-joined
- AD organizational structure created (OUs, groups, users)
- Ubuntu Server VM deployed and configured

---

## Build Log

### Windows Server VM
#### VM Creation
- ISO: Windows Server 2022 Evaluation
- RAM: 6GB
- vCPUs: 2 
- Disk: 60GB
- Network: NAT
- Edition: Standard Evaluation
![](Attatchments%20/Pasted%20image%2020260312091924.png)
#### Network Configuration
- Static IP: 192.168.122.200
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.122.1
- DNS: 127.0.0.1
#### Server Configuration
- Hostname: DC01
- Domain: homelab.local
#### Active Directory
- Forest/Domain: homelab.local
- Domain Controller: DC01
- Promotion: Successful
- NetBIOS Name: HOMELAB
#### DNS
- Verified: dcdiag /test:dns - Passed
#### DHCP
- Scope: 192.168.122.0/24
- Range: 192.168.122.100 - 192.168.122.199
- Gateway: 192.168.122.1
- DNS: 192.168.122.200

### Windows 11 Client VM 
#### VM Creation 
- ISO: Windows 11
- RAM: 4GB 
- vCPUs: 2 
- Disk: 50GB - 
- Network: NAT 
- Edition: Windows 11 Pro
![](Attatchments%20/Pasted%20image%2020260312103223.png)
### Ubuntu Server VM
#### VM Creation
- ISO: Ubuntu Server 24.04
- RAM: 4096 MB (4GB)
- vCPUs: 2
- Disk: 40GB
- Network: NAT
- Edition: Ubuntu Server 24.04
![](Attatchments%20/Pasted%20image%2020260312104929.png)
--- 
## Notes
[Anything learned, gotchas, or worth remembering from this phase.]

---
## Troubleshooting

See issue log: [DHCP-001](../Troubleshooting/Issues-Log.md) | DHCP New Scope Greyed Out/unlickable in Server Console

Unable to add new scope through console
![](Attatchments%20/Pasted%20image%2020260312130408.png)
Didn't change anything in DHCP Console
![](Attatchments%20/Pasted%20image%2020260312130102.png)
Manually added scope
![](Attatchments%20/Pasted%20image%2020260312130656.png)
Success 
![](Attatchments%20/Pasted%20image%2020260312130734.png)