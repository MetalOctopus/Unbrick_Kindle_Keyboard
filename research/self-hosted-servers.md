# Self-Hosted Book Server Options

## Calibre-Web (Recommended)

**Docker:** `linuxserver/calibre-web` — available in Unraid Community Apps, actively maintained, multiarch.

**Key features for this project:**
- OPDS enabled by default at `/opds`
- **`/basic` endpoint** — stripped-down, no-JS interface designed for Kindle's experimental browser (merged PR #3008, late 2024)
- On-the-fly EPUB → MOBI/AZW3 conversion (if Calibre binaries installed in container)
- Send-to-Kindle via email (if Amazon services are reachable — they're not for K3)
- Web upload for adding books from any browser
- User auth, reading progress tracking

**Kindle 3 compatibility:**
- Stock browser: can use `/basic` over **plain HTTP** only (TLS broken)
- KOReader OPDS: works with both HTTP and HTTPS (KOReader has modern TLS)
- Content-Type must be `application/octet-stream` for stock browser downloads (known quirk, issue #1149)

**Calibre-Web Automated (CWA):** `crocodilestick/calibre-web-automated`
- Wraps Calibre-Web with auto-import from a watched folder
- Auto-converts formats on ingest
- v2.1.0 fixed Unraid/NAS compatibility
- Drop an EPUB into `/imports` on Unraid share → auto-ingested and converted

## COPS (Calibre OPDS PHP Server)

**Status:** Original (seblucas) archived. Active fork: `mikespub-org/seblucas-cops` — latest v4.5.2 (June 2026), requires PHP 8.4+.

**Docker:** `linuxserver/cops` in Unraid Community Apps.

**Features:** Purpose-built for OPDS. Also serves HTML web interface. Lighter than Calibre-Web.

**Limitations vs Calibre-Web:** No send-to-Kindle, no on-the-fly conversion, no Kindle-friendly `/basic` UI.

**OPDS feed URL:** Changed in v3.x from `feed.php` to `index.php/feed`.

## Kavita

**Docker:** `kizaing/kavita` in Unraid Community Apps.

**Problem for K3:** Does NOT natively support MOBI/AZW3. Supports EPUB, PDF, CBZ, CBR. Stock Kindle can't read EPUB. Only viable if jailbroken with KOReader (which reads EPUB natively).

**OPDS:** Yes, has OPDS support.

**Send-to-Kindle:** Has it, but Amazon now converts EPUB → KFX, which K3 may not support.

## KOReader + OPDS (on jailbroken Kindle)

**This is the best pairing with any server.**

- Built-in OPDS client in KOReader
- Add catalog: Search icon → OPDS catalog → "+" → enter URL (e.g. `http://server:8083/opds/`)
- **Include trailing slash** or it won't connect
- Browse by author, title, newest; tap to download
- Works with Calibre-Web, COPS, Kavita, BookShelves, Librarr

**Calibre Wireless Device Connection:**
- KOReader can also appear as a wireless Calibre device
- File Manager → Customizations → Calibre → Wireless settings → Enable
- Calibre desktop sees it as a connected device over WiFi
- Send books as if USB-connected

## Simple HTTP File Server

Dead-simple fallback: any HTTP server (nginx, Python `http.server`, Flask) serving a directory of .mobi files.

**Stock Kindle browser** can navigate to `http://ip:port/`, see file listings, download `.mobi`/`.azw`/`.prc`/`.txt`.

**Requirements:** Plain HTTP only, `Content-Type: application/octet-stream`.

**KindleServer** (https://github.com/edgartaor/kindleServer): Flask app with UI designed for Kindle experimental browser.

## Phone-Based Server (for airplanes)

Run a simple HTTP server app on the phone. Kindle connects to phone hotspot, downloads from `http://192.168.43.1:PORT/`.

No home server or internet needed. Works fully offline.

## Syncthing

Can be installed on jailbroken Kindles for peer-to-peer file sync. Combined with KOReader's progress sync, enables full self-hosted reading workflow across devices.

## Unraid Community Apps (Book-Related)

| App | Docker Image | Notes |
|-----|-------------|-------|
| Calibre-Web | `linuxserver/calibre-web` | Best for this project |
| Calibre-Web Automated | `crocodilestick/calibre-web-automated` | Auto-import/convert |
| COPS | `linuxserver/cops` | Lightweight OPDS |
| Kavita | `kizaing/kavita` | Modern UI, no MOBI |
| Calibre (full) | `linuxserver/calibre` | Full GUI via browser VNC |
| Ubooquity | various | Lightweight comics + ebooks |
| Shelfmark | - | Aggregates book downloads |
