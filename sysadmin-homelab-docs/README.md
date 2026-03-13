# Homelab Project Roadmap
**Neff Clark Jr.** | IT Generalist / Junior Sysadmin Portfolio Project

---

## Project Overview

This project documents the design, deployment, and administration of a simulated small business IT environment built entirely on a local Linux desktop using KVM/QEMU virtualization. The goal is to demonstrate hands-on sysadmin and IT support skills in a realistic, multi-system Windows domain environment.

The lab was built to bridge the gap between certification knowledge and practical administrative experience, targeting IT Help Desk, Desktop Support, IT Generalist, and Junior Sysadmin roles.

---

## Host Environment

| Component | Detail |
|---|---|
| Host OS | Pop!_OS (Linux) |
| Hypervisor | KVM/QEMU + Virt-Manager |
| RAM | 32GB |
| Storage | 2TB SSD |
| Documentation | Obsidian MD → GitHub |

---

## Technology Stack

| Technology | Role |
|---|---|
| Windows Server 2022 | Domain Controller, AD, DNS, DHCP |
| Windows 10/11 | Domain-joined client workstation |
| Ubuntu Server | Linux VM, hosts osTicket ticketing system |
| Active Directory | User, group, and OU management |
| Group Policy (GPO) | Policy enforcement across domain |
| osTicket | Open source helpdesk ticketing system |
| PowerShell | Automation and admin scripting |
| Bash | Linux administration scripting |
| GitHub | Version control, script storage, public portfolio |

---

## Project Phases

### Phase 0 — Foundation
**Goal:** Prepare the host environment and documentation structure before any VMs are deployed.

**Deliverables:**
- KVM/QEMU + Virt-Manager installed and verified on Pop!_OS
- Obsidian vault created with folder structure established
- GitHub repository initialized
- Windows Server 2022, Windows 11, and Ubuntu Server ISOs downloaded

---

### Phase 1 — Core Infrastructure
**Goal:** Deploy and configure the core virtual infrastructure including a Windows domain environment and Linux server.

**Deliverables:**
- Windows Server 2022 VM deployed and configured
- Server promoted to Domain Controller
- Active Directory, DNS, and DHCP operational
- Windows 11 client VM deployed and domain-joined
- AD organizational structure created (OUs, groups, users)
- Ubuntu Server VM deployed and configured
---

### Phase 2 — Sysadmin Scenarios
**Goal:** Simulate real-world IT administration tasks performed in a managed domain environment.

**Deliverables:**
- Group Policies configured and enforced (password policy, desktop restrictions, software control)
- File shares created with NTFS permissions mapped to AD groups
- User lifecycle workflows documented (onboarding, password reset, offboarding)
- Common helpdesk scenarios simulated and documented (locked accounts, mapped drives, profile issues)
- Ubuntu Server VM basic Linux administration performed

---

### Phase 3 — Automation & Scripting
**Goal:** Demonstrate ability to automate repetitive administrative tasks.

**Deliverables:**
- PowerShell script: Bulk user creation from CSV
- PowerShell script: Automated user onboarding (create account, assign group, set home folder)
- PowerShell script: Account audit (last logon, disabled accounts)
- Bash script: Basic Ubuntu Server administration tasks
- All scripts pushed to GitHub with clear README documentation

---

### Phase 4 — Ticketing System
**Goal:** Deploy and use a helpdesk ticketing system to demonstrate IT workflow knowledge.

**Deliverables:**
- osTicket deployed on Ubuntu Server (Apache, PHP, MariaDB stack)
- Ticket categories and workflows configured
- End-to-end ticket resolutions documented for scenarios from Phase 2
- Ticketing workflow write-up included in Obsidian documentation

---

### Phase 5 — Documentation & Portfolio Polish
**Goal:** Present the project professionally for employers and make it publicly accessible.

**Deliverables:**
- Obsidian vault fully written up (network diagram, runbooks, build log, troubleshooting notes)
- GitHub repo with clean README explaining the project at a glance
- Resume updated to reflect lab project and skills demonstrated
- (Optional) MkDocs site deployed via GitHub Pages

---
## Project Status Tracker

- [x] [[Phase-0-Foundation|Phase 0 — Foundation]]
- [x] [[Phase-1-Core-Infrastructure|Phase 1 — Core Infrastructure]]
- [ ] [[Phase-2-Sysadmin-Scenarios|Phase 2 — Sysadmin Scenarios]]
- [ ] [[Phase-3-Automation-Scripting|Phase 3 — Automation & Scripting]]
- [ ] [[Phase-4-Ticketing-System|Phase 4 — Ticketing System]]
- [ ] [[Phase-5-Documentation-Polish|Phase 5 — Documentation & Polish]]