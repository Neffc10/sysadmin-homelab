# Phase 1 -- Core Infrastructure
## Contents
- [Goal](#Goal)
- [Deliverables](#Deliverables)
- [Build Log](#Build-Log)
- [Notes](#Notes)
- [Troubleshooting](#Troubleshooting)
## Goal
Deploy and configure the core virtual infrastructure including a Windows domain environment and Linux server.

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
![](Attatchments%20/Pasted%20image%2020260313102852.png)
### Windows 11 Client VM 
#### VM Creation 
- ISO: Windows 11
- RAM: 4GB 
- vCPUs: 2 
- Disk: 50GB - 
- Network: NAT 
- Edition: Windows 11 Pro
![](Attatchments%20/Pasted%20image%2020260312103223.png)
#### Network Configuration 
- IP: DHCP
- DNS: 192.168.122.200 (DC01)
- DNS set and verified via ipconfig & ping
![](Attatchments%20/Pasted%20image%2020260313101711.png)
#### Domain Join
- Domain: homelab.local
- Domain join verified with systeminfo domain and Windows Server ADUC
![](Attatchments%20/Pasted%20image%2020260313104121.png)
![](Attatchments%20/Pasted%20image%2020260313104333.png)
### Ubuntu Server VM
#### VM Creation
- ISO: Ubuntu Server 24.04
- RAM: 4096 MB (4GB)
- vCPUs: 2
- Disk: 40GB
- Network: NAT
- Edition: Ubuntu Server 24.04
![](Attatchments%20/Pasted%20image%2020260312104929.png)
#### Network Configuration
- Static IP: 192.168.122.50/24
- Gateway: 192.168.122.1
- DNS: 192.168.122.200 (DC01)
![](Attatchments%20/Pasted%20image%2020260313114713.png)
#### /etc/netplan/50-cloud-init.yaml
- dhcp4: no
- Static address set to 192.168.122.50/24
- Default route via 192.168.122.1
- Nameserver set to 192.168.122.200
![](Attatchments%20/Pasted%20image%2020260313114843.png)
#### /etc/systemd/resolved.conf
- DNS=192.168.122.200
- Domains=homelab.local
![](Attatchments%20/Pasted%20image%2020260313114028.png)
#### DNS Verification
- nslookup homelab.local resolved successfully
- Resolver: systemd-resolved stub (127.0.0.53) forwarding to DC01
- Status: Operational
![](Attatchments%20/Pasted%20image%2020260313114048.png)

### Active Directory Structure
#### Organizational Units
- Homelab (top level) 
	- IT 
	- HR 
	- Finance 
	- Computers
#### Users
- ituser01(IT)
- hruser01(HR)
- finuser01(Finance)
![](Attatchments%20/Pasted%20image%2020260313120118.png)
#### Groups 
- IT-Users (Global, Security) -- member: ituser01 
- HR-Users (Global, Security) -- member: hruser01 
- FIN-Users (Global, Security) -- member: finuser01
![](Attatchments%20/Pasted%20image%2020260313120736.png)

#### Computers 
- Windows 11 client moved to Homelab: Computers OU
![](Attatchments%20/Pasted%20image%2020260313121232.png)

--- 
## Notes

- Windows 11 Add-Computer command failed with invalid character error. Domain join completed successfully via GUI instead.
- Ubuntu Server received IP 192.168.122.7 from KVM NAT DHCP before Windows Server DHCP was configured Static IP set manually via netplan.
- Ping homelab.local fails from Ubuntu potentially due to Windows Firewall blocking ICMP -- DNS resolution confirmed working via nslookup instead

---
## Troubleshooting

#### DHCP New Scope Greyed Out/unlickable in Server Console
See issue log: [DHCP-001](../Troubleshooting/Issues-Log.md)

Unable to add new scope through console
![](Attatchments%20/Pasted%20image%2020260312130408.png)
Starting & stopping DHCP didn't fix issue
![](Attatchments%20/Pasted%20image%2020260312130102.png)
Manually added scope
![](Attatchments%20/Pasted%20image%2020260312130656.png)
Success 
![](Attatchments%20/Pasted%20image%2020260312130734.png)

#### Ubuntu Server Not Resolving homelab.local
See issue log: [DNS-001](../Troubleshooting/Issues-Log.md)

Resolvectl showing DC01 (192.168.122.200) as the DNS server, 
`nslookup homelab.local` failed with "temporary failure in name resolution."

System was falling back to the systemd-resolved stub (127.0.0.53) without forwarding to DC01. Fixed by manually configuring /etc/systemd/resolved.conf.

