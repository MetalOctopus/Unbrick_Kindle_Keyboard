# Unbrick Kindle Keyboard

## Project Goal
Restore wireless book delivery to a Kindle Keyboard (3rd Gen, K3) after Amazon killed TLS/cloud connectivity. The end state is: user searches Anna's Archive from the Kindle itself, downloads books over phone hotspot, reads them in KOReader.

## Communication Style
- Never end responses with engagement questions ("Want me to?", "Should I?", "Which do you prefer?")
- State information and recommendations directly. User will direct next steps.

## Writing Files to Samba/Network Shares
The Write tool fails with EACCES on samba/CIFS mounts. Use `cat > /path << 'EOF'` via Bash instead.

## Key Context
- **Device:** Kindle Keyboard 3rd Gen (2010). Serial prefixes: B006 (3G+WiFi), B008 (WiFi), B00A (International 3G). Firmware 3.x (final: 3.4.3). 256 MB RAM. ARM926EJ-S processor. 2.4 GHz WiFi only, WPA2 only.
- **The Problem:** Amazon deprecated TLS 1.0/1.1, the Kindle 3 can't do TLS 1.2+, so all Amazon cloud services are dead. Store, Send-to-Kindle email, 3G — all gone.
- **User's Server:** Unraid at home with Docker capability. GitHub: MetalOctopus.
- **User's Workflow:** Downloads books on phone, wants to get them onto Kindle wirelessly (especially on planes via phone hotspot).
- **The Kindle case:** User has the Amazon case with built-in hinge-powered LED light. It's hardware-only, unaffected by any software changes.

## Solution Architecture

### Primary Path (jailbreak + KOReader + Anna's Archive plugin)
1. Jailbreak K3 via NiLuJe's legacy jailbreak
2. Install MKK → DevCerts → KUAL → MRPI → KOReader (kindle-legacy) → annas.koplugin
3. KOReader has its own modern TLS stack, bypassing the stock Kindle's TLS limitation
4. annas.koplugin lets user search/download from Anna's Archive directly on device
5. Full guide in `guide.html` and detailed research in `research/`

### Fallback Path (if TLS still fails in KOReader on K3)
1. Calibre-Web on Unraid (Docker: `linuxserver/calibre-web` or `crocodilestick/calibre-web-automated`)
2. Served over plain HTTP (bypasses TLS entirely)
3. KOReader's OPDS client browses the catalog, or stock browser uses `/basic` endpoint
4. Remote access via Tailscale/WireGuard for on-the-go use

### Simplest Fallback (no server needed)
1. HTTP server app on phone serving a local book folder
2. Kindle connects to phone hotspot
3. Downloads .mobi via experimental browser or KOReader from `http://192.168.43.1:PORT/`

## Working Method (how we build this)
- This repo is a living, field-tested guide. Walk each step on a REAL device, confirm it, then write it up. "Confirmed" = observed on the test device; label anything not yet seen as expected/unverified.
- After each verified step: update `guide.html` + `README.md` + `CHECKLIST.md` to match reality, log it in `FIELD-NOTES.md`, then make a focused commit and `git push origin main` (the `origin` remote carries a push token — redact it in any echoed output).
- **Verify-then-document:** inspect actual archive contents (real filenames, magic bytes, `sha256sum`) before writing instructions. The original guide had real drift (wrong filenames, `.zip` vs `.tar.xz`, an obsolete rename step). Pin files by exact discriminator (`k3g-B006`, never a `k3g*` glob — it also matches `k3gb`).
- **Audience = non-technical, no LLM, scared of bricking.** Keep docs incredibly verbose and hand-holding, DIY-first, with "what success looks like" + recovery at every step. Mirror EVERY required file into `mirror/` (with `SHA256SUMS` + provenance) so nothing rots.

## Device Access (this WSL session)
- Kindle plugs into the Windows host; reaches WSL via drvfs as removable drive **`G:`** (label "Kindle"; letter can vary — check `Get-Volume` via powershell.exe).
- Mount: `sudo -n mount -t drvfs G: /mnt/g` (a passwordless sudo rule for mount/umount is installed at `/etc/sudoers.d/kindle-mount`). The mount goes stale after reboots — remount. After each flash the Kindle leaves USB drive mode; the user must reconnect before remounting.
- `sha256sum` every file after copying to the Kindle. Serial/firmware/keystore are NOT on the USB partition.

## Current Progress & Verified Learnings (2026-06, device: B006 / FW 3.4.3)
- **Steps 1–5 CONFIRMED on-device** (jailbreak → MKK → DevCerts → block OTA → KUAL launches). See `FIELD-NOTES.md` for the blow-by-blow. Steps 7–8 documented, not yet device-confirmed.
- **Jailbreak proof:** after the flash, the `.bin` is consumed and a `linkjail/` folder appears on the root.
- **KUAL cert-family rule (the big gotcha):** KUAL must match the installed cert family. We use **NiLuJe DevCerts-20250419 + NiLuJe 2025 KUAL** (`mirror/niluje/KUAL-KDK-1.0.azw2`, ~131.0 KB). The KindleModding KUAL (`mirror/kindlemodding/`, ~131.7 KB) is the **Hotfix** family — mixing it with DevCerts gives "not signed by a registered developer." The 2022 KUAL (~127.8 KB) is dead (cert expired 2025-04-17).
- **DevCerts K3 filename uses a HYPHEN:** `Update-mkk-20250419-k3g-B006_keystore-install.bin` (underscore is only the k4/k5 files).
- **MRPI (Step 6) is NOT needed for KOReader** — KOReader ships its own KUAL launcher. Treat it as optional/skippable.
- Files live on NiLuJe's OVH index (`storage.gra.cloud.ovh.net/.../mr-public/`, listing disabled but `index.html` + direct files work); DevCerts is a MobileRead t=225030 attachment, not on that index.

## Key Unknowns (as of June 2026)
- **TLS on kindle-legacy KOReader:** Nobody has publicly confirmed that KOReader's bundled curl on the kindle-legacy build can negotiate TLS 1.2+ with Anna's Archive and LibGen mirrors. This is the biggest risk. If it fails, fall back to plain HTTP via Calibre-Web.
- **RAM on K3:** 256 MB is tight. The annas.koplugin does HTML scraping via regex which should be lightweight, but heavy search results could OOM. Use "no framework" launch mode.
- **Tailscale on K3:** ARM926EJ-S is very old. Tailscale requires ARMv5+ static binary. Theoretically possible, unconfirmed.

## File Structure
- `README.md` — The main guide / GitHub front page: verbose, hand-holding, non-technical-friendly, with direct download links.
- `guide.html` — Styled web version of the guide (deployed at https://verygneiss.au/kindlebreak/).
- `CHECKLIST.md` — One-page print-and-tick checklist of all steps + success indicators.
- `FIELD-NOTES.md` — Chronological real-device log (source of truth for progress); one chapter per phase, with the gotchas we hit.
- `mirror/` — Every required file, archived with `SHA256SUMS` + provenance (`mirror/README.md`). Subdirs: `niluje/`, `devcerts/`, `koreader/`, `annas-koplugin/`, `kindlemodding/`.
- `research/` — Background research notes.
- `CLAUDE.md` — This file (context for Claude Code).

## Important Links
- NiLuJe's MobileRead thread (ALL jailbreak downloads): https://www.mobileread.com/forums/showthread.php?t=225030
- KOReader releases (kindle-legacy): https://github.com/koreader/koreader/releases
- annas.koplugin (upstream): https://github.com/fischer-hub/annas.koplugin
- KindleModding.org K3 jailbreak: https://kindlemodding.org/jailbreaking/Legacy/K2DXDXGK3-Jailbreak/
- Calibre-Web Docker: https://github.com/linuxserver/docker-calibre-web
- Calibre-Web Automated: https://github.com/crocodilestick/calibre-web-automated
- Anna's Archive current domains (check Wikipedia): https://en.wikipedia.org/wiki/Anna%27s_Archive
