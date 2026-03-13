# Issues Log

---
### IMG-001 | Obsidian images not rendering on GitHub

**Date:** 2026-03-10
**Phase:** Phase 0 — Foundation
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
**Phase:** Phase 1 — Core Infrastructure
**Status:** Resolved

**Symptom:** New Scope option was greyed out and unclickable in the DHCP console after installing the DHCP Server role and completing DHCP configuration.

**Cause:** Likely a DHCP console display/refresh bug following initial server authorization. Console failed to update state even after service
restart and multiple relaunches.

**Resolution:** Created scope manually via command line:
`netsh dhcp server 192.168.122.200 add scope 192.168.122.0 255.255.255.0 "Homelab Scope"`
This unstuck the console and New Scope became clickable afterward.
Scope options and activation completed through GUI normally.

## [ID] | [Issue Title]

**Date:**
**Phase:**
**Status:**

**Symptom:**

**Cause:**

**Resolution:**
