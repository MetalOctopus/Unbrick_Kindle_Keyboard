# Kindle 3 Jailbreak & Post-Jailbreak Ecosystem

## Jailbreak Method

The K3 runs firmware 3.x (separate line from modern 5.x Kindles). Modern jailbreaks (WinterBreak, AdBreak, SpringBreak, LanguageBreak) do NOT apply — those target firmware 5.x.

**The method: NiLuJe K2/DX/DXG/K3 Jailbreak**
- Supports firmware 3.0 through 3.4.4
- Different .bin files for firmware 3.0-3.2 vs 3.3-3.4.x
- Files named `Update_jailbreak_k3[variant]_install.bin`
- Variants: k3g (B006, 3G+WiFi), k3w (B008, WiFi), k3gb (B00A, International 3G)
- Source: NiLuJe's MobileRead snapshot thread (https://www.mobileread.com/forums/showthread.php?t=225030)

**Process:** Copy .bin to Kindle root via USB → Eject → Home → Menu → Settings → Menu → Update Your Kindle → Reboot

## Post-Jailbreak Stack (install order matters)

### 1. MKK (MobileRead Kindlet Kit)
- Required for pre-K5 devices to run Java Kindlets
- File: `kindle-mkk-20141129-r18833.tar.xz`
- Same install process as jailbreak (.bin to root, Update Your Kindle)

### 2. DevCerts (Developer Certificates) — CRITICAL
- Original dev certs expired **April 17, 2025**
- Without updated certs, KUAL shows "permissions expired" errors
- Fix: `DevCerts-20250419-KeyStore.zip` from NiLuJe
- Contains model-specific .bin files with `keystore` in the name
- NiLuJe released this fix within days of expiry

### 3. OTA Update Blocker
- Simplest method: create a **folder** named `update.bin.tmp.partial` on Kindle root
- Folder's existence prevents OTA staging
- Alternative: `kindle-kual-blockamazon` KUAL extension
- Alternative: fill storage to ~50-90 MB free

### 4. KUAL (Kindle Unified Application Launcher)
- For K3: use `KUAL-KDK-1.0.azw2` (legacy/KDK variant, NOT PEKI)
- Goes in `documents/` folder, appears as a "book" in library
- Opening it launches a menu for homebrew apps

### 5. MRPI (MobileRead Package Installer)
- Companion to KUAL, handles extension discovery
- Copy `extensions/` and `mrpackages/` to Kindle root
- Needs ~220 MB free space

### 6. KOReader
- **Must use kindle-legacy package** (covers K2, DX, K3)
- Regular "kindle" build targets newer ARM — wrong architecture for K3
- Copy `extensions/` and `koreader/` to Kindle root
- Launch via KUAL → "Start KOReader (no framework)" recommended (frees RAM)
- Current version: v2025.04
- Supports: EPUB, MOBI, PDF, DJVU, CBZ, FB2, PDB, TXT, HTML, RTF, CHM, DOC
- Has built-in OPDS client, modern TLS stack, Calibre wireless integration
- Navigation on K3 via D-pad and physical keyboard (no touchscreen needed)
- KOReader issue #11295 improved D-pad support

### 7. USBNetwork (optional, for SSH)
- Enables SSH over USB (default IP: 192.168.15.244) or WiFi
- Activate by typing `;un` in Kindle search bar
- Config: `/mnt/us/usbnet/etc/config`
- Useful for advanced modifications, DNS fixes, etc.

## Other Available Software (K3 Ecosystem)

From the MobileRead K3 Index (https://wiki.mobileread.com/wiki/K3_Index):
- **Audio:** MPlayer (OGG/WAV/MP3/FLAC/AAC), Kinamp, audiobook players
- **Games:** Chess, Minesweeper, GoMoku, interactive fiction (Frotz)
- **Alt readers:** Duokan, CoolReader 3, FBreader
- **Dev tools:** Terminal/bash, Perl, Tiny C compiler, JS interpreter
- **Networking:** Kindle HTTP server, Mutt email, VNC client, WPA-EAP WiFi
- **Utilities:** Calculator, eMonitor (secondary display), KindleNote
- **KindleForge:** On-device package manager
- **Custom screensavers:** Place 600x800 PNG/JPEG in `linkss/screensavers/`
- **Tailscale:** KUAL extension exists (https://github.com/mitanshu7/tailscale_kual) but K3 compatibility unconfirmed due to old ARM architecture

## TLS/SSL Situation

**The core problem:** K3 ships OpenSSL 0.9.8j, only supports TLS 1.0/1.1. All modern services require TLS 1.2+.

**Can TLS be upgraded on stock firmware?** Community consensus: no.
- ARM926EJ-S too slow for TLS 1.2 in software
- OpenSSL 0.9.8 → 1.x breaks ABI (different soname)
- Amazon declined to update

**Workarounds attempted:**
1. Updating CA certificates (mixed results — TLS version still too old)
2. Correct device date (some cert validation is time-related)
3. **KOReader** — ships its own modern TLS stack. Best practical workaround.
4. Tailscale proxy mode (routes through tailnet)

**Bottom line:** Stock browser is dead for HTTPS. KOReader's networking is the way forward.

## Community Resources

- **MobileRead forums** — central hub, Kindle Developer's Corner active
- **NiLuJe** — most prolific contributor, maintains jailbreak tools, KUAL, USBNetwork
- **KindleModding.org** — comprehensive maintained guides
- **KindleModShelf.me** — organized mod catalog
- **GitHub:** `spekulazarus/kindle-revival`, `koreader/koreader`
- **XDA Forums** has a K3 thread
- Community is small but dedicated. Legacy Kindle support maintained through 2025-2026.
