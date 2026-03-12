# Phase 0 — Foundation
## Contents
- [Goal](#Goal)
- [Deliverables](#Deliverables)
- [Build Log](#Build-Log)
- [Notes](#Notes)
- [Troubleshooting](#Troubleshooting)
## Goal
Prepare the host environment for VM depolyment
## Deliverables
- KVM/QEMU + Virt-Manager installed and verified on Pop!OS
- Obsidian vault created with folder structure established
- GitHub repository initialized
- Windows Server 2022, Windows 11, and Ubuntu Server ISOs downloaded

---
## Build Log
### KVM, QEMU, and Virt-Manager Installation
Update system, install KVM, QEMU, and Virt-Manager, add user to groups.
![](Attatchments%20/Pasted%20image%2020260311115746.png)

Launch Virt-Manager.
![](Attatchments%20/Pasted%20image%2020260311120303.png)

### Obsidian to GitHub Image Config
Configure Obsidian to render images correctly in both Obsidian and GitHub.
- Settings → Files & Links 
- Default location for new attachments: Subfolder under current folder 
- Link format: Path relative to current file 
- Wikilinks: Off
![](Attatchments%20/Pasted%20image%2020260311120723.png)

### GitHub Repository Setup
Create a public repository to host the project documentation and scripts.

- **sysadmin-homelab** — contains project README and Obsidian documentation vault

Configured SSH key authentication for secure pushing from the local machine.
![](Attatchments%20/Pasted%20image%2020260311123849.png)

### ISO Downloads
Download installation media for all three virtual machines.

| OS                  | Version              |
| ------------------- | -------------------- |
| Windows Server 2022 | Evaluation (180-day) |
| Windows 11          | Disk Image           |
| Ubuntu Server       | 24.04 LTS            |

---
## Notes
- Windows Server 2022 and Windows 11 are available as free downloads directly 
  from Microsoft — no license required for lab/evaluation use.
- KVM/QEMU is preferred over VirtualBox for better performance with Windows VMs 
  and is more representative of production virtualization environments.
- Obsidian wikilink format is incompatible with GitHub markdown rendering — 
  standard relative path format must be used for images to display correctly 
  in both environments.
- SSH key authentication is more secure and convenient than password/token 
  based authentication for GitHub.

---
## Troubleshooting
[[Issues-Log#IMG-001]] | Obsidian images not rendering on GitHub