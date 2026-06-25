# Kindle 3 Hardware & Technical Constraints

## Specifications

| Spec | Value |
|------|-------|
| Released | 2010 |
| Display | 6" E Ink Pearl, 600x800, 167 ppi, 16-level grayscale |
| Processor | ARM926EJ-S (ARMv5TEJ) — very old, very slow by modern standards |
| RAM | 256 MB |
| Storage | 4 GB (~3 GB user available) |
| WiFi | 802.11b/g, 2.4 GHz only |
| WiFi Security | WPA2 only (NO WPA3, NO 5 GHz) |
| USB | Micro-B |
| Audio | Stereo speakers, 3.5mm headphone jack |
| Input | Physical QWERTY keyboard, 5-way D-pad, page turn buttons |
| Battery | ~1 month with WiFi off |
| Backlight | None (requires external light) |
| Touchscreen | None |

## Model Variants

| Serial Prefix | Model Code | Description |
|--------------|------------|-------------|
| B006 | K3G | Kindle Keyboard 3G + WiFi |
| B008 | K3W | Kindle Keyboard WiFi-only |
| B00A | K3GB | Kindle Keyboard 3G International |

## Firmware

- Ships with various 3.x versions
- Final official firmware: **3.4.3**
- Jailbreak supports 3.0 through 3.4.4
- Completely separate firmware line from modern 5.x Kindles

## TLS/SSL Problem

**Root cause:** Ships with OpenSSL 0.9.8j, supports only TLS 1.0 and 1.1.

**Impact:** Can't connect to any modern HTTPS service. Amazon Store, Send-to-Kindle, 3G gateway — all dead. The experimental browser can't load most websites.

**Why it can't be fixed on stock firmware:**
- ARM926EJ-S reportedly too slow for TLS 1.2 in software
- OpenSSL 0.9.8 → 1.x requires ABI changes (different soname) that break everything
- Amazon officially declined to update
- Modifying system files breaks firmware manifest checksums, risks bricking on OTA

**KOReader workaround:** KOReader bundles its own curl and OpenSSL libraries with modern TLS support. This is independent of the stock Kindle's TLS stack. On the kindle-legacy build, this *should* work but is unconfirmed specifically on K3 hardware.

## WiFi Constraints

**Critical for phone hotspot setup:**
- 2.4 GHz ONLY — phone hotspot must not be set to 5 GHz or "auto" (may prefer 5 GHz)
- WPA2-PSK ONLY — no WPA3, no WPA2/WPA3 mixed mode
- Simple passwords recommended (no special characters)
- 802.11b/g speeds — large files (PDFs) will be slow

## Memory Constraints

- 256 MB total RAM
- Stock Kindle GUI consumes significant RAM
- **"No framework" launch mode** in KOReader kills stock GUI to free memory
- Keep searches specific to avoid OOM from heavy HTML parsing
- KOReader on K3 is functional but slower than on modern devices

## Input (No Touchscreen)

The K3 has no touchscreen. All interaction via:
- **5-way D-pad** — up/down/left/right/center for navigation and selection
- **Physical QWERTY keyboard** — text input (actually an advantage for searching)
- **Page turn buttons** — physical buttons on left and right bezels
- **Menu button** — opens context menus
- **Back button** — navigation back
- **Home button** — return to home screen

KOReader's UI widgets (Menu, InputDialog, ConfirmBox, ButtonDialog, TextViewer) all support D-pad/keyboard navigation. Issue #11295 improved D-pad support in newer versions.

## The Amazon Case with Built-in Light

The official Amazon Kindle Keyboard case has an LED reading light that extends from the top of the case. It draws power from the Kindle through a **physical hinge connector** — metal contacts in the case hinge that mate with contacts on the Kindle body.

**This is pure hardware.** The light turns on when:
1. The case cover is open
2. The Kindle is powered on

No software involvement. Jailbreaking, KOReader, or any other software modification has zero effect on the light. It works exactly the same before and after.

## USB File System Layout

When connected via USB, the Kindle mounts as a drive with this structure:

```
Kindle root/
├── documents/          ← books go here (and KUAL-KDK-1.0.azw2)
├── audible/
├── music/
├── system/             ← don't touch
├── extensions/         ← KUAL extensions (MRPI, KOReader launcher)
├── mrpackages/         ← MRPI packages
├── koreader/           ← KOReader installation
│   └── plugins/        ← KOReader plugins (annas.koplugin goes here)
└── update.bin.tmp.partial/  ← OTA blocker (folder, not file)
```

## Recovery

- **Hard reboot:** Hold power slider 30+ seconds
- **USB recovery:** If device mounts as USB drive, delete problematic .bin files and reboot
- **USB serial recovery:** Hardware-level recovery mode accessible via serial connection — can restore even from botched firmware. Would need to deliberately destroy bootloader to truly brick.
- **Factory reset:** Settings menu restores stock firmware (also removes jailbreak)
