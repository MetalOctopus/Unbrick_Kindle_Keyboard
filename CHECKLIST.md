# ✅ Kindle Keyboard Rescue — Print-and-Tick Checklist

Print this page (or keep it open) and tick each box as you go. It's the whole journey on one
sheet. **Every step has detailed, hand-holding instructions in [README.md](README.md)** — come
back here to keep your place.

**How far this is proven:** Steps 0–5 have been done and confirmed on a real **B006 / firmware
3.4.3** Kindle. Steps 7–8 are documented and being tested. Other models (B008, B00A) use the
identical steps with their own file.

**Golden rules:** ① Don't factory-reset the Kindle. ② Always pick the file that matches YOUR
serial. ③ If "Update Your Kindle" is greyed out, you used the wrong file — no harm, just redo
with the right one. ④ Take your time.

---

## ☐ Before you start
- [ ] Kindle Keyboard + its USB cable + a computer, ~30 minutes
- [ ] Downloaded the files I need from this repo's **[`mirror/`](mirror/)** folder (each step links its file in the README)

## ☐ Step 0 — Which Kindle do I have? (DO NOT skip)
- [ ] On the Kindle: **Home → Menu → Settings**
- [ ] Serial starts with **B006**, **B008**, or **B00A** *(if not → STOP, this guide isn't for your Kindle)*
- [ ] Firmware is **3.0–3.4.3**
- [ ] I wrote my model down → **B006 = `k3g` · B008 = `k3w` · B00A = `k3gb`**

---

### 🔁 The "flash" pattern used in Steps 1, 2, 3
**Plug in → copy the file to the Kindle's main drive (the "root") → safely eject → on the
Kindle: Home → Menu → Settings → Menu → "Update Your Kindle" → let it reboot.**

## ☐ Step 1 — Jailbreak
- [ ] Flashed **`Update_jailbreak_0.13.N_<my-model>_install.bin`** *(use the `-3.0-to-3.2` version only if firmware ≤ 3.2)*
- [ ] **Looks right when:** Kindle reboots normally. *(Proof: over USB, the `.bin` is gone and a `linkjail` folder appeared.)*

## ☐ Step 2 — MKK
- [ ] Flashed **`Update_mkk-20141129-<my-model>_install.bin`**
- [ ] **Looks right when:** reboots, **no visible change** (that's normal)

## ☐ Step 3 — DevCerts (refresh expired certificates)
- [ ] Flashed **`Update-mkk-20250419-<my-model>_keystore-install.bin`** ⚠️ note the **dash** after `Update`
- [ ] **Looks right when:** reboots, **no visible change** (normal). *This is the last "Update Your Kindle" for a while.*

## ☐ Step 4 — Block Amazon updates *(no flash, no reboot)*
- [ ] In the Kindle's main drive (root), created an **empty folder** named exactly: `update.bin.tmp.partial`
- [ ] **Looks right when:** the folder is sitting there. *(Keep Airplane Mode on when not using WiFi.)*

## ☐ Step 5 — KUAL (the apps menu) 🎉 the "it's alive" moment
- [ ] Copied **`KUAL-KDK-1.0.azw2`** (from **`mirror/niluje/`** — see README's warning on using the right one!) into the Kindle's **`documents`** folder *(NOT the root)*
- [ ] Ejected → Home → opened the new **KUAL** "book"
- [ ] **Looks right when:** a small **menu** opens (looks nearly empty — that's normal; it fills up after KOReader)
- [ ] *If "not signed by a registered developer":* use the `mirror/niluje/` KUAL, restart the Kindle, retry — see README Step 5

## ☐ Step 6 — MRPI — **OPTIONAL, you can skip it**
- [ ] *Not needed for KOReader.* Only do this if some other add-on you want specifically asks for MRPI.

## ☐ Step 7 — KOReader (your new reading app) 📖
- [ ] Copied the **`koreader`** and **`extensions`** folders (from the KOReader zip) to the Kindle's **root** — merge if asked
- [ ] Opened **KUAL → KOReader → "Start KOReader (no framework)"**
- [ ] **Looks right when:** a clean file-browser screen appears that looks nothing like the normal Kindle

## ☐ Step 8 — Anna's Archive plugin (search & download books on the Kindle)
- [ ] Copied the **`annas.koplugin`** folder into **`koreader/plugins/`** on the Kindle
- [ ] Opened KOReader (KUAL → KOReader → no framework) → **Search** menu
- [ ] **Looks right when:** **"Anna's Archive"** appears in the Search menu

---

## ☐ Using it — the airplane workflow
- [ ] Phone hotspot ON — **2.4 GHz + WPA2 only** (no 5 GHz / WPA3)
- [ ] Kindle WiFi → connect to the hotspot
- [ ] **KUAL → KOReader (no framework) → Search → Anna's Archive →** type a title → pick **EPUB** → download → read 🎉

---

*Stuck? Every step's "what if it goes wrong" is in [README.md](README.md). Worst realistic case
is a greyed-out menu (wrong file) — you cannot permanently break the Kindle with these steps.*
