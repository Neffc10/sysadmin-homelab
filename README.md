# sysadmin-homelab

A virtualized small business IT environment built from scratch on a Linux desktop, designed to demonstrate hands-on experience with Windows Server, Active Directory, and IT support ticket workflows.

## Overview

This lab simulates a real-world managed IT environment including a Windows domain, user administration, Group Policy, file shares, helpdesk ticketing, and scripted automation. It was built as a portfolio project targeting IT Help Desk, Desktop Support, IT Generalist, and Junior Sysadmin roles.

## Technology Stack

| Technology | Role |
|---|---|
| Pop!_OS (Linux) | Host OS |
| KVM/QEMU + Virt-Manager | Hypervisor |
| Windows Server 2022 | Domain Controller, AD, DNS, DHCP |
| Windows 10/11 | Domain-joined client workstation |
| Ubuntu Server | Linux VM, osTicket ticketing system |
| Active Directory | User, group, and OU management |
| Group Policy (GPO) | Policy enforcement across domain |
| osTicket | Open source helpdesk ticketing system |
| PowerShell | Automation and admin scripting |
| Bash | Linux administration scripting |

## Documentation

Full project documentation including build logs, runbooks, and troubleshooting notes is maintained in the [sysadmin-homelab-docs](./sysadmin-homelab-docs) folder of this repository.

## Author

**Neff Clark Jr.**
[LinkedIn](https://www.linkedin.com/in/neff-clark-jr) | [GitHub](https://github.com/Neffc10)