# Unbrick Kindle Keyboard (3rd Gen)

Amazon killed TLS 1.0/1.1 support on their servers, effectively bricking the Kindle Keyboard's wireless features. No store, no Send-to-Kindle, no 3G, no cloud sync. This project documents how to jailbreak the device, install KOReader, and search/download books from Anna's Archive directly on the Kindle over a phone hotspot.

> ## ✅ Is this for your device? (read this first)
>
> **This guide is for the Kindle Keyboard (3rd Gen / "K3") only.** It has been walked
> end-to-end and **verified on a real device: model `B006` (3G + WiFi, US), firmware
> `3.4.3`** — every step confirmed on hardware and logged in [`FIELD-NOTES.md`](FIELD-NOTES.md).
>
> **Check yours:** on the Kindle, **Home → Menu → Settings**. Note the **serial prefix**
> (first 4 characters) and the **firmware version** at the bottom.
>
> | Your device | Status |
> |-------------|--------|
> | Serial `B006` + firmware `3.4.3` | ✅ Exact field-tested path — should match step for step |
> | Serial `B006`/`B008`/`B00A`, firmware `3.0`–`3.4.3` | ✅ Supported — identical steps, pick your variant's file (all three listed at each step); documented but not yet independently field-tested |
> | Serial **not** `B006`/`B008`/`B00A` | ❌ Not your device — this is K3-only. See [KindleModding.org](https://kindlemodding.org/) |
>
> Throughout this repo, **"confirmed"** means we saw it work on the B006/3.4.3 unit;
> anything not yet observed on hardware is labelled as such, so you always know what's
> proven vs. expected. **All required files are mirrored in [`mirror/`](mirror/)** — you
> can complete the whole process from this repo alone, no dead forum links.

## What This Gets You

- **KOReader** replacing the stock reader — supports EPUB, PDF, DJVU, MOBI, and dozens more formats
- **Anna's Archive search** directly on the Kindle via the annas.koplugin
- **OPDS catalog browsing** for self-hosted libraries (Calibre-Web, COPS, etc.)
- **Modern TLS** via KOReader's bundled curl (bypasses the stock Kindle's broken TLS stack)
- **No Amazon dependency whatsoever**

## The Device

| Spec | Detail |
|------|--------|
| Model | Kindle Keyboard (3rd Gen, 2010) |
| Display | 6" E Ink Pearl, 600x800, 167 ppi |
| Processor | ARM926EJ-S (ARMv5TEJ) |
| RAM | 256 MB |
| Storage | 4 GB (~3 GB usable) |
| WiFi | 2.4 GHz only, WPA2 only |
| Firmware | 3.0 — 3.4.3 |
| Serial prefixes | B006 (3G+WiFi), B008 (WiFi), B00A (International 3G) |

## Quick Start

See `guide.html` for the full step-by-step with success/failure indicators at each step.

**TL;DR — 8 steps, all via USB:**

1. **Jailbreak** — NiLuJe's kindle-jailbreak-0.13.N
2. **MKK** — MobileRead Kindlet Kit (required for K3)
3. **DevCerts** — Updated developer certificates (old ones expired April 2025)
4. **Block OTA** — Create `update.bin.tmp.partial` folder on Kindle root
5. **KUAL** — App launcher (appears as a "book")
6. **MRPI** — Package installer for KUAL extensions
7. **KOReader** — Alternative reader (kindle-legacy build)
8. **annas.koplugin** — Anna's Archive search/download plugin

## Usage Workflow (airplane mode)

1. Phone hotspot on (2.4 GHz, WPA2)
2. Kindle connects to hotspot
3. KUAL → KOReader (no framework mode)
4. Search → Anna's Archive → type query → pick EPUB → download → read

## Fallback: Self-Hosted Library

If KOReader's TLS can't reach Anna's Archive on the K3 (unconfirmed as of June 2026):

- **Calibre-Web** on Unraid/Docker (`linuxserver/calibre-web`) served over plain HTTP
- KOReader's OPDS client browses the catalog at `http://server:8083/opds/`
- Or stock Kindle browser hits `http://server:8083/basic` (Kindle-friendly interface)
- Remote access via Tailscale/WireGuard for on-the-go use

## Bricking Risk

Essentially zero for true brick. The K3 has USB serial recovery. The only real risk is using the wrong `.bin` file for your model variant — causes a soft brick recoverable by holding power 30 seconds or deleting the .bin via USB. Triple-check your serial prefix.

## Downloads

All jailbreak components from one thread:
- **[NiLuJe's MobileRead Snapshot Thread](https://www.mobileread.com/forums/showthread.php?t=225030)** — jailbreak, MKK, DevCerts, KUAL, MRPI

Other downloads:
- **[KOReader kindle-legacy](https://github.com/koreader/koreader/releases)** — look for `koreader-kindle-legacy-*.zip`
- **[annas.koplugin](https://github.com/fischer-hub/annas.koplugin/releases)** — Anna's Archive plugin

## Research

Detailed research notes in `research/`:
- `jailbreak.md` — Jailbreak methods, community state, post-jailbreak software ecosystem
- `self-hosted-servers.md` — Calibre-Web, COPS, Kavita, KOReader OPDS, and alternatives
- `annas-archive.md` — Anna's Archive integration tools, plugins, current legal/domain status
- `kindle3-hardware.md` — K3 hardware constraints, TLS situation, WiFi limitations

## Links

| Resource | URL |
|----------|-----|
| NiLuJe's Thread | https://www.mobileread.com/forums/showthread.php?t=225030 |
| KOReader Releases | https://github.com/koreader/koreader/releases |
| annas.koplugin | https://github.com/fischer-hub/annas.koplugin |
| KindleModding.org (K3) | https://kindlemodding.org/jailbreaking/Legacy/K2DXDXGK3-Jailbreak/ |
| KOReader Kindle Wiki | https://github.com/koreader/koreader/wiki/Installation-on-Kindle-devices |
| MobileRead K3 Index | https://wiki.mobileread.com/wiki/K3_Index |
| Calibre-Web Docker | https://github.com/linuxserver/docker-calibre-web |
| Calibre-Web Automated | https://github.com/crocodilestick/calibre-web-automated |
| Anna's Archive Domains | https://en.wikipedia.org/wiki/Anna%27s_Archive |
