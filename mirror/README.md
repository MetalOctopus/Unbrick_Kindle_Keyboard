# mirror/ — Archived files (everything you need, kept forever)

**Every file the guide depends on is mirrored here.** You can complete the entire rescue
using only this folder — no forum account, no hunting dead links, no LLM. These Kindles
will outlive their software's hosting; this folder is the insurance.

> Verify any copy against the recorded hashes: `sha256sum -c SHA256SUMS` (run from this
> `mirror/` directory).

## What's here

| File | Step | What it is | Covers |
|------|------|-----------|--------|
| `niluje/kindle-jailbreak-0.13.N-r18833.tar.xz` | 1 | NiLuJe's jailbreak | **All** legacy models (K2/DX/DXG/**K3**), all firmware |
| `niluje/kindle-mkk-20141129-r18833.tar.xz` | 2 | MobileRead Kindlet Kit (run Java apps) | All K3 variants |
| `devcerts/DevCerts-20250419-KeyStore.zip` | 3 | **Updated dev certs** (originals expired 2025-04-17) | All K3 variants + K2/DX/K4/K5 |
| `niluje/KUAL-KDK-1.0.azw2` | 5 | **KUAL app (NiLuJe 2025) — USE THIS** ✅ matches DevCerts; confirmed on B006/3.4.3 | K3 legacy |
| `niluje/KUAL-v2.7.37-gfcb45b5-20250419.tar.xz` | 5 | Full NiLuJe 2025 KUAL bundle (the `.azw2` above is extracted from this) | K3 legacy |
| `niluje/KUAL-v2.7.29-g7750a3a-20221017.tar.xz` | 5 | OLD 2022 KUAL — cert **expired 2025-04-17**; reference only, do NOT use | K3 legacy |
| `kindlemodding/KUAL-KDK-1.0.azw2` | 5 (alt) | KUAL for the **Hotfix** path — different cert family, use ONLY with the hotfix below | K3 legacy |
| `kindlemodding/Update_hotfix_universal.bin` | 5 (alt) | Hotfix 2.5.0 — date-proof certs; alternative cert path (K3 lightly tested) | all |
| `niluje/kual-mrinstaller-1.7.N-r18983.tar.xz` | 6 *(optional)* | MRPI package installer — **not needed for KOReader**, skip unless another add-on requires it | K3 (has `bin/K3/`) |
| `koreader/koreader-kindle-legacy-v2026.03.zip` | 7 | KOReader reader (modern TLS, OPDS) | `kindle-legacy` = K2–K4 |
| `annas-koplugin/annas.koplugin-FIXED-dcb859a08f54.zip` | 8 | **Anna's Archive search+download plugin (USE THIS)** ✅ fixed scraper, current domains | any KOReader |
| `annas-koplugin/annas.koplugin-main-dcb859a08f54.tar.gz` | 8 | Full pinned source the FIXED zip was built from (provenance) | — |
| `annas-koplugin/annas.koplugin-v0.1.8.zip` | 8 | ❌ official release — **downloads BROKEN** (stale scraper, pre domain-seizure); reference only | any KOReader |

The single jailbreak tarball (Step 1) contains the `.bin` for **every** legacy device and
both firmware ranges — so any K2/DX/DXG/K3 owner can pull this one file and find theirs.

## Which file is mine? (K3 — by serial prefix)

Check **Home → Menu → Settings** on the Kindle; note the serial prefix and firmware.

| Serial | Model | Jailbreak `.bin` (FW 3.3.x/3.4.x) | Jailbreak `.bin` (FW ≤ 3.2) | DevCerts `.bin` |
|--------|-------|-----------------------------------|------------------------------|-----------------|
| `B006` | K3 3G US (k3g) | `Update_jailbreak_0.13.N_k3g_install.bin` | `..._k3g-3.0-to-3.2_install.bin` | `Update-mkk-20250419-k3g-B006_keystore-install.bin` |
| `B008` | K3 WiFi (k3w) | `Update_jailbreak_0.13.N_k3w_install.bin` | `..._k3w-3.0-to-3.2_install.bin` | `Update-mkk-20250419-k3w-B008_keystore-install.bin` |
| `B00A` | K3 3G Intl (k3gb) | `Update_jailbreak_0.13.N_k3gb_install.bin` | `..._k3gb-3.0-to-3.2_install.bin` | `Update-mkk-20250419-k3gb-B00A_keystore-install.bin` |

(These `.bin`s live *inside* the archives above — extract, pick yours by the table.)

## Provenance

- **`niluje/`** — retrieved 2026-06-25 from NiLuJe's public storage
  (`storage.gra.cloud.ovh.net/v1/AUTH_2ac4bfee353948ec8ea7fd1710574097/mr-public/`,
  the "NiLuJe's Stuff" index). Jailbreak from `Legacy/`, MKK from `Touch/`, KUAL + MRPI
  from `KUAL/`.
- **`devcerts/`** — retrieved 2026-06-25 from MobileRead thread t=225030 attachment
  (`attachment.php?attachmentid=215127&d=1745098511`), filename
  `DevCerts-20250419-KeyStore.zip`. The 2025-04-19 keystore refresh after the 2025-04-17
  cert expiry. Not hosted on the OVH index or KindleModding GitHub — the forum attachment
  is the authoritative source.
- **`koreader/`** — KOReader `v2026.03`, the `kindle-legacy` build, from the official
  GitHub release (`github.com/koreader/koreader/releases`).
- **`niluje/KUAL-KDK-1.0.azw2` + `KUAL-v2.7.37-gfcb45b5-20250419.tar.xz`** — retrieved
  2026-06-25 from NiLuJe's `mr-public/KUAL/`. The 2025 re-signed KUAL whose signature matches
  the `DevCerts-20250419` keystore. **This is the combination we confirmed launches KUAL on a
  real B006/3.4.3 device.** The standalone `.azw2` is just extracted from the tarball for
  one-click use.
- **`kindlemodding/`** — retrieved 2026-06-25. `KUAL-KDK-1.0.azw2` (131,667 B) from
  KindleModding's install-KUAL guide and `Update_hotfix_universal.bin` (Hotfix 2.5.0,
  3,743,762 B) from `github.com/KindleModding/Hotfix`. These are an **alternative cert
  family**: the KindleModding KUAL is signed for the Hotfix's keys (valid 1970–9999,
  clock-drift-proof), **not** for NiLuJe's DevCerts. Use them together as a fallback path —
  do NOT pair this KUAL with DevCerts (that mismatch is exactly what gave us "not signed by a
  registered developer"). Hotfix is only lightly tested on K3.
- **`annas-koplugin/`** — retrieved 2026-06-26 from `github.com/fischer-hub/annas.koplugin`.
  The official **v0.1.8 release downloads are BROKEN**: Anna's Archive had a domain seized and
  changed its site, and v0.1.8's scraper predates the fix (search works, but you get "No
  download link available"). The author's **main branch** fixes it (rewritten `src/scraper.lua`
  with current domains + LibGen.li `ads.php?md5=` download extraction) but isn't released yet.
  So we packaged the main branch **pinned to commit `dcb859a08f5429613b382b06f390b40944d76fc3`**
  as `annas.koplugin-FIXED-dcb859a08f54.zip` (correctly-named folder, README screenshots
  stripped to keep it small) — **this is the one to use**. The full source tarball is kept
  alongside for provenance, and the broken v0.1.8 is kept only for reference.

## Verified gotchas (so the guide stays honest)

- Jailbreak `.bin` names include the version: `Update_jailbreak_0.13.N_k3g_install.bin`.
- DevCerts K3 `.bin` uses a **hyphen**: `Update-mkk-20250419-k3g-B006_keystore-install.bin`
  (the k4/k5 files in the same zip use an underscore — don't let that confuse you).
- `-3.0-to-3.2` jailbreak variants are for FW ≤ 3.2 **only**; FW ≥ 3.3 uses the plain file.
- These `.bin`s are genuine signed Kindle update packages (magic header `FC02`).
