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

## Key Unknowns (as of June 2026)
- **TLS on kindle-legacy KOReader:** Nobody has publicly confirmed that KOReader's bundled curl on the kindle-legacy build can negotiate TLS 1.2+ with Anna's Archive and LibGen mirrors. This is the biggest risk. If it fails, fall back to plain HTTP via Calibre-Web.
- **RAM on K3:** 256 MB is tight. The annas.koplugin does HTML scraping via regex which should be lightweight, but heavy search results could OOM. Use "no framework" launch mode.
- **Tailscale on K3:** ARM926EJ-S is very old. Tailscale requires ARMv5+ static binary. Theoretically possible, unconfirmed.

## File Structure
- `guide.html` — Step-by-step jailbreak + setup guide (deployable as a webpage)
- `research/` — Detailed research notes from investigation
- `CLAUDE.md` — This file (context for Claude Code)
- `README.md` — Project overview and quick reference

## Important Links
- NiLuJe's MobileRead thread (ALL jailbreak downloads): https://www.mobileread.com/forums/showthread.php?t=225030
- KOReader releases (kindle-legacy): https://github.com/koreader/koreader/releases
- annas.koplugin (upstream): https://github.com/fischer-hub/annas.koplugin
- KindleModding.org K3 jailbreak: https://kindlemodding.org/jailbreaking/Legacy/K2DXDXGK3-Jailbreak/
- Calibre-Web Docker: https://github.com/linuxserver/docker-calibre-web
- Calibre-Web Automated: https://github.com/crocodilestick/calibre-web-automated
- Anna's Archive current domains (check Wikipedia): https://en.wikipedia.org/wiki/Anna%27s_Archive
