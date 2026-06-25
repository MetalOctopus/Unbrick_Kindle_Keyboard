# mirror/ — Archived jailbreak components

These are **local copies of the upstream files** the guide depends on, kept here so the
rescue procedure survives even if the original hosts disappear. The whole point of this
project is that these Kindles will outlive their software's hosting — so we mirror.

> **Do not trust a link you can't re-download in 20 years.** Every file the guide tells
> you to fetch should eventually live here, with its source URL, retrieval date, and a
> SHA-256 so a future user can verify integrity.

## Provenance & integrity

Retrieved **2026-06-25** from NiLuJe's public object storage
(`storage.gra.cloud.ovh.net/.../mr-public/`, the "NiLuJe's Stuff" index — the canonical
home of the legacy Kindle jailbreak). Verify any copy with `sha256sum -c SHA256SUMS`.

### `niluje/` — from NiLuJe's mr-public

| File | Upstream path (under `mr-public/`) | Used by | SHA-256 |
|------|-----------------------------------|---------|---------|
| `kindle-jailbreak-0.13.N-r18833.tar.xz` | `Legacy/` | Step 1 (jailbreak) | `8f5c8a78e3c4574232acf4783da1c66959078a4e10116c30cd40b16fb98e3ac3` |
| `kindle-mkk-20141129-r18833.tar.xz` | `Touch/` | Step 2 (MKK) | `3d7289f1ddcf18cebb67053cd33ac5ecd7b4a8116bd11d3c75dd6f220a7d8d9d` |
| `KUAL-v2.7.29-g7750a3a-20221017.tar.xz` | `KUAL/` | Step 5 (KUAL) | `bc193e4e954631930b8e58a22881ee690b8f5b73eeb713d27f74e5ab923d5303` |
| `kual-mrinstaller-1.7.N-r18983.tar.xz` | `KUAL/` | Step 6 (MRPI) | `dd24ebe74da300eb0799710377f0219cac6cd3dccbe5847ace4d89efe5bcdcb9` |

Version on the live index (2026-06-25): jailbreak `0.13.N @ r18833`, dated 2023-Jan-04.

### Notes / discrepancies vs. the guide as written

- **Filenames carry the version.** The actual jailbreak `.bin` inside the tarball is
  `Update_jailbreak_0.13.N_k3g_install.bin`, **not** `Update_jailbreak_k3g_install.bin`.
- **Firmware split is explicit.** NiLuJe ships two K3 variants per model: a plain one and
  a `-3.0-to-3.2` one. The `-3.0-to-3.2` files are for FW **≤ 3.2 only**; FW **3.3.x/3.4.x**
  (our 3.4.3) uses the **plain** `k3g` file. Using the wrong one greys out "Update Your
  Kindle" — the guide's only real soft-brick failure mode.
- **KUAL/MRPI here are older** (`v2.7.29` / `r18983`) than the versions named in the
  guide (`v2.7.37` / `r19303`). These are what the public index currently serves; the
  newer builds (and the mandatory **DevCerts/keystore** for Step 3, post April-2025 cert
  expiry) are not in this index and will be sourced + mirrored separately when we reach
  those steps.

## Still to mirror

- [ ] DevCerts / updated keystore (Step 3) — mandatory; originals expired 2025-04-17.
- [ ] KOReader `kindle-legacy` build (Step 7) — large (~tens of MB); from KOReader GitHub releases.
- [ ] `annas.koplugin` (Step 8) — from fischer-hub GitHub releases.
- [ ] Newer KUAL / MRPI, if the device run shows the older ones misbehave.
