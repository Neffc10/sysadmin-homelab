# Issues Log

---
### IMG-001 | Obsidian images not rendering on GitHub

**Date:** 2026-03-10
**Phase:** Phase 0 -- Foundation
**Status:** Resolved

**Symptom:**
Images pasted into Obsidian notes were not rendering when viewed on GitHub.

**Cause:**
Obsidian's default wikilink format and attachment path settings are not compatible with GitHub's markdown renderer.

**Resolution:**
Changed the following in Settings → Files & Links:
- Default location for new attachments: Subfolder under current folder
- Link format: Path relative to current file
- Wikilinks: Off

### DHCP-001 | DHCP New Scope Greyed Out/Unlickable in Server Console

**Date:** 2026-03-12
**Phase:** Phase 1 -- Core Infrastructure
**Status:** Resolved

**Symptom:** New Scope option was greyed out and unclickable in the DHCP console after installing the DHCP Server role and completing DHCP configuration.

**Cause:** Likely a DHCP console display/refresh bug following initial server authorization. Console failed to update state even after service
restart and multiple relaunches.

**Resolution:** Created scope manually via command line:
`netsh dhcp server 192.168.122.200 add scope 192.168.122.0 255.255.255.0 "Homelab Scope"`
This unstuck the console and New Scope became clickable afterward.
Scope options and activation completed through GUI normally.

### DNS-001 | Ubuntu Server Not Resolving homelab.local via System Resolver

**Date:** 2026-03-13
**Phase:** Phase 1 
**Status:** Resolved

**Symptom:** `nslookup homelab.local` failed with "temporary failure in name resolution" despite resolvectl showing correct DNS server (192.168.122.200).

**Cause:** systemd-resolved was using its local stub resolver (127.0.0.53) and not forwarding queries to DC01. Netplan DNS configuration alone was insufficient to configure systemd-resolved's forwarding behavior.

**Resolution:** 
Edited /etc/systemd/resolved.conf: 
DNS=192.168.122.200 
Domains=homelab.local 
Then ran: `sudo systemctl restart systemd-resolved`

**References**: 
- /etc/netplan/50-cloud-init.yaml 
- /etc/systemd/resolved.conf

### GPO-001 | Desktop Lockdown GPO linked to domain root

**Date:** 2026-04-01 
**Phase:** Phase 2 
**Status:** Resolved

**Symptom:** Windows Settings app would flash and close immediately on DC01. Remote Desktop could not be enabled via Server Manager due to a restrictions popup.

**Cause:** Desktop Lockdown GPO was linked to the domain root (homelab.local) instead of the Computers OU, causing it to apply to DC01 and the Administrator account.

**Resolution:** Removed the GPO link from homelab.local via Group Policy Management. Re-linked the Desktop Lockdown GPO to the Computers OU. Ran `gpupdate /force` on DC01 to apply the corrected policy.

**References:**
* Group Policy Management Console
* Computers OU: OU=Computers,OU=Homelab,DC=homelab,DC=local