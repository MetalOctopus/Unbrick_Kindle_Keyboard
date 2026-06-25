# Anna's Archive Integration

## Current State (June 2026)

**Collection:** 64.4M books, 95.7M papers, ~1.1 PB in torrents.

**Legal situation — severe:**
- Jan 2026: .org domain suspended (Spotify-related lawsuit, preliminary injunction)
- Mar 2026: .li domain permanently deleted
- May 2026: $19.5M default judgment from 13 major publishers (SDNY), global domain takedown ordered
- Telegram channel suspended in 2025
- DNS moved from Cloudflare to DDoS-Guard (Russian provider)
- Blocked by ISPs in Italy, Netherlands, UK, Belgium, Germany

**Currently working domains (June 2026):**
- `annas-archive.gl` (Greenland)
- `annas-archive.pk` (Pakistan)
- `annas-archive.gd` (Grenada)
- Check Wikipedia for latest: https://en.wikipedia.org/wiki/Anna%27s_Archive

**API:** JSON API available with paid membership (donation). Secret key from account page. Third-party RapidAPI wrapper exists (3,000 free monthly requests).

## Calibre Plugins

### calibre_annas_archive (ScottBot10) — Established
- 248 stars, Python
- Adds Anna's Archive as a Calibre "store"
- Search with filters (file type, language, source), download directly
- Configurable mirror priority and download verification
- Install: download zip from GitHub releases → Preferences → Plugins
- Last updated Nov 2024, still functional
- https://github.com/ScottBot10/calibre_annas_archive

### cal-annas (a-peirogon) — Newer
- 23 stars, Python, v0.3.2 (June 21, 2026)
- Same concept, configurable filters, real-time uptime data via SLUM
- https://github.com/a-peirogon/cal-annas

**No metadata-only plugin exists.** Calibre's creator said no moral issue with using AA for metadata, won't include in core due to legal status, nothing prevents third-party. None built yet.

## KOReader Plugin

### annas.koplugin
- **Upstream:** https://github.com/fischer-hub/annas.koplugin (fischer-hub)
- **Fork:** https://github.com/norator3000/annas.koplugin
- Current version: v0.1.8 (March 2, 2025)
- No API key/account/login required — scrapes public web interface

**How it works:**
1. Auto-resolves current Anna's Archive domain by scraping Wikipedia (cached 12h)
2. Constructs search URL with query, language, format, sort filters
3. Parses HTML via regex for book metadata (title, author, format, MD5)
4. Downloads through Library Genesis mirrors (`.la`, `.gl`, `.li`, `.is`, `.rs`, `.st`, `.bz`)
5. Saves file in binary mode to configured download directory

**HTTP fallback chain:**
1. `curl -L -s --max-time 20` (most reliable)
2. `wget`
3. KOReader's built-in `socket.http` (LuaSocket)

**Configuration:**
- Download directory
- Language filter (30 languages)
- Format filter: AZW, AZW3, CBZ, DJV, DJVU, EPUB, FB2, LIT, MOBI, PDF, RTF, TXT
- Sort order: Most Relevant, Newest, Oldest, Largest, Smallest, Newest/Oldest Added, Random
- WiFi off after download toggle
- Timeout settings (Search: 15s, Download: 15s block/infinite total)
- Base URL override
- DNS workaround note: change to 1.1.1.1 if resolution fails

**Installation:**
1. Download `annas.plugin.zip` from releases
2. Extract, rename folder: `annas.koplugin-0.1.8` → `annas.koplugin`
3. Copy to `koreader/plugins/annas.koplugin/` on Kindle
4. Restart KOReader

**Limitations:**
- HTML scraper is fragile — breaks when AA changes layout
- Domain resolution depends on Wikipedia scraping
- LibGen mirror availability unpredictable
- Tested only on Kindle Paperwhite 11th gen
- KOReader feature request (#12597) was rejected — maintainers want single-service plugins in koreader/contrib, not main repo

**K3-specific concerns:**
- Plugin UI uses standard KOReader widgets (Menu, InputDialog, ConfirmBox, ButtonDialog, TextViewer) — all D-pad/keyboard navigable
- Physical QWERTY keyboard is actually an advantage for search input
- HTML scraping via regex should be lightweight enough for 256 MB RAM
- Biggest unknown: TLS compatibility of kindle-legacy bundled curl

## *arr-Style Automation Tools

### Librarr (226 stars, Go, updated June 2026)
- "The missing *arr for books"
- Searches 13+ sources in parallel, auto-imports into Calibre (calibredb), Audiobookshelf, Kavita, Komga
- Built-in OPDS 1.2 feed
- Prowlarr support, Torznab/Newznab APIs
- ~17 MB binary, ~14 MB idle memory
- Request/approval workflows, series auto-complete, author monitoring
- https://github.com/JeremiahM37/librarr

### Shelfarr (215 stars, Ruby, updated June 2026)
- Like Jellyseerr for books
- Direct downloads from Anna's Archive and Z-Library (no torrent client needed)
- Role-based multi-user with 2FA/SSO
- https://github.com/Pedro-Revez-Silva/shelfarr

### Stacks (749 stars, updated March 2026)
- Dedicated Anna's Archive download manager
- Docker Compose, password-protected web UI (port 7788)
- Real-time progress, auto mirror fallback, download resume
- Tampermonkey script adds download buttons to AA pages
- FlareSolverr integration for Cloudflare bypass
- https://github.com/zelestcarlyone/stacks

### Shelfmark (3.4k stars, formerly calibre-web-automated-book-downloader)
- Web interface for searching/requesting books → feeds into CWA ingest
- "Stable but not under active maintenance" as of May 2026
- https://github.com/calibrain/shelfmark

### Luma (3 stars, TypeScript, Dec 2025)
- Self-hosted library with built-in e-reader and audiobook player
- Built-in Anna's Archive search, Google Books, Open Library, OPDS
- Imports existing Calibre libraries
- https://github.com/netpersona/Luma

**Note:** Readarr (the long-standing *arr for books) is officially retired as of 2026.

## Browser Extensions

- **GoodLIB** (360 stars, Chrome + Firefox): One-click search on Goodreads/StoryGraph pages to Anna's Archive, Z-Library, Gutenberg
- **To Anna's Archive** (Firefox): Extracts DOI, searches Anna's Archive SciDB

## CLI Tools

- **annas-mcp** (908 stars, Go): MCP server + CLI. `book-search`, `book-download`. Requires paid AA membership for JSON API.
- **AnnaChive** (Go): Multi-source downloader with Tor integration
- **anna-dl** (Python): Simple downloader, libgen mirrors only
- **Openlib** (2.4k stars, Dart): Mobile app for shadow libraries

## OPDS from Anna's Archive

No mature OPDS server for Anna's Archive exists. Best approach:
1. Use download tools (Stacks, Librarr, CLI) to populate a Calibre library
2. Serve that library via OPDS using Calibre-Web, COPS, or Librarr's built-in OPDS

Librarr's built-in OPDS 1.2 feed is the closest to a direct bridge.
