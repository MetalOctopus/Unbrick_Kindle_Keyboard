# Bring Your Kindle Keyboard Back to Life 📖

Amazon quietly switched off the servers your old Kindle Keyboard talks to. That's why the
store, "Send to Kindle", 3G, and syncing all stopped working — the device itself is
perfectly fine, Amazon just stopped answering the phone.

**This guide fixes that.** By the end, your Kindle will let you search for and download
books straight from the device over your phone's hotspot — no Amazon account, no computer
needed once it's set up. We'll go **one tiny step at a time**, and at every step we'll tell
you **exactly what you'll see on the screen when it worked**, so you're never guessing.

> **You do not need to be technical to do this.** If you can copy a file onto a USB drive,
> you can do this. Every file you need is already in this guide (linked below) — you won't
> have to go hunting through old forums. Take your time. There's no rush and nothing here
> is a race.

> 🖨️ **Want a simple tick-box version to print and follow?** See
> **[CHECKLIST.md](CHECKLIST.md)** — the whole process on one page, with a box for each step
> and what success looks like. Use it to keep your place; come back here for the detail.

---

## 🛑 First: "Will this break my Kindle?" — please read, it'll calm your nerves

Short answer: **almost certainly not, and you can undo all of it.** Here's the honest truth,
because being scared usually comes from not knowing what's actually at stake:

- **You cannot truly "brick" (permanently kill) your Kindle with these steps.** The Kindle
  has a built-in recovery system. Nothing in this guide touches the deep part of the device
  that would be needed to permanently destroy it.
- **It's reversible.** If you ever want your normal Kindle back, a factory reset (in the
  Kindle's own Settings) returns it to stock. Your device is not being changed forever.
- **You're not losing anything.** Amazon already turned off all the online features. There's
  nothing left to lose — we're only adding things back.
- **The one mistake that matters is easy to avoid:** using the file for the *wrong Kindle
  model*. If you do, the Kindle simply **refuses** to install it (a menu option goes grey) —
  it does **not** damage anything. You just delete that file and use the right one. We tell
  you exactly which file is yours in [Step 0](#step-0--which-kindle-do-you-have-do-not-skip-this).
- **If a screen ever looks stuck:** hold the power switch for **30 seconds** to force a
  restart. The Kindle is almost certainly fine. (More in [If something goes wrong](#-if-something-goes-wrong).)

So: breathe. Worst realistic case is "a menu option is greyed out and I redo it with the
right file." That's it.

---

## 📋 What you'll need

- Your **Kindle Keyboard** (the one with the physical keyboard at the bottom, from ~2010).
- The **USB cable** that charges it (the small "micro-USB" end goes into the Kindle).
- A **computer** (Windows, Mac, or Linux — anything that can copy files to a USB drive).
- About **30 minutes**. You can stop and resume between steps; nothing has to be done in one sitting.
- ⚠️ **Do NOT factory reset or "wipe" the Kindle** before or during this. Just leave it as-is.

---

## Step 0 — Which Kindle do you have? (DO NOT skip this)

This is the single most important check. Using the right file for *your exact model* is what
keeps everything safe and smooth.

**On the Kindle**, press the **Home** button, then **Menu**, then choose **Settings**. Look
at the screen:

- The **Serial Number** is listed there. You only care about the **first 4 characters**.
- The **Firmware Version** is written along the **bottom edge** of the Settings screen, like
  `Kindle 3.4.3`.

Now find your row:

| First 4 of serial | Your model | Firmware 3.0–3.4.3? | Is this guide for you? |
|---|---|---|---|
| **B006** | Kindle Keyboard 3G + WiFi (US) | yes | ✅ **Yes** — and `B006` + `3.4.3` is the exact setup we tested on a real device |
| **B008** | Kindle Keyboard WiFi-only | yes | ✅ Yes — same steps, just your model's file |
| **B00A** | Kindle Keyboard 3G International | yes | ✅ Yes — same steps, just your model's file |
| anything else | a different Kindle | — | ❌ **Stop.** This guide is only for the Kindle Keyboard. For other Kindles, see [KindleModding.org](https://kindlemodding.org/) |

> 📝 **Write your model down** (B006, B008, or B00A). You'll pick the file with that code in
> it at Steps 1, 2, and 3. **`k3g` = B006, `k3w` = B008, `k3gb` = B00A.** Note that `k3g`
> and `k3gb` look almost identical — match yours **exactly**.

**Honest status:** every step below was done and confirmed on a real **B006 / firmware 3.4.3**
Kindle. The B008 and B00A models follow the *identical* steps with their own file; those files
are included and labeled, but we haven't personally tested those two models yet. Wherever
something is "expected" rather than "we watched it happen," we say so.

---

## 🗣️ A few words you'll see (in plain English)

- **Jailbreak** — unlocking the Kindle so it can run helpful software Amazon didn't allow.
  Harmless and reversible.
- **The "root" of the Kindle** — when you plug the Kindle into your computer, it shows up
  like a USB stick. The **root** just means the *top level* of that drive — not inside any
  folder. "Copy it to the root" = drop it in the main window that opens, loose, not in
  `documents` or anywhere else.
- **`.bin` file** — a little installer file. You copy it to the Kindle, then tell the Kindle
  to install it using its own "Update Your Kindle" menu.
- **"Flash" / "install"** — same thing here: letting the Kindle install one of those files.
- **Safely eject** — telling your computer "I'm done with this USB drive" before you unplug,
  so the file finishes copying. (On Windows: click the little USB icon near the clock →
  "Eject Kindle". On Mac: drag the Kindle to the trash / click the eject arrow.)
- **KUAL** — a simple menu of extra apps that will appear on your Kindle later.
- **KOReader** — the new, better reading app we're installing. It's what you'll actually read in.

---

## 📦 All your files are right here — you don't have to find anything

Everything is stored in this repository so it can't disappear on you. **Click to download:**

| Used in | Click to download | (the original home, if you're curious) |
|---|---|---|
| Step 1 | **[Jailbreak file](mirror/niluje/kindle-jailbreak-0.13.N-r18833.tar.xz)** | [NiLuJe's page](https://www.mobileread.com/forums/showthread.php?t=225030) |
| Step 2 | **[MKK file](mirror/niluje/kindle-mkk-20141129-r18833.tar.xz)** | [NiLuJe's page](https://www.mobileread.com/forums/showthread.php?t=225030) |
| Step 3 | **[DevCerts file](mirror/devcerts/DevCerts-20250419-KeyStore.zip)** | [NiLuJe's page](https://www.mobileread.com/forums/showthread.php?t=225030) |
| Step 5 | **[KUAL app (KUAL-KDK-1.0.azw2)](mirror/niluje/KUAL-KDK-1.0.azw2)** — NiLuJe 2025, matches DevCerts ✅ | [NiLuJe (MobileRead)](https://www.mobileread.com/forums/showthread.php?t=225030) |
| Step 6 | **[MRPI file](mirror/niluje/kual-mrinstaller-1.7.N-r18983.tar.xz)** | [NiLuJe's page](https://www.mobileread.com/forums/showthread.php?t=225030) |
| Step 7 | **[KOReader file](mirror/koreader/koreader-kindle-legacy-v2026.03.zip)** | [KOReader downloads](https://github.com/koreader/koreader/releases) |
| Step 8 | **[Anna's Archive plugin](mirror/annas-koplugin/annas.koplugin-v0.1.8.zip)** | [Plugin downloads](https://github.com/fischer-hub/annas.koplugin/releases) |

These files end in `.tar.xz` or `.zip`. They're like ZIP folders — you'll need to **unzip
(extract)** them on your computer first. Windows can open `.zip` on its own; for `.tar.xz`,
the free program [7-Zip](https://www.7-zip.org/) opens them (you may need to extract twice —
once to get a `.tar`, once more to get the files).

---

## 🔁 The pattern you'll repeat (read this once — Steps 1, 2, and 3 all work this way)

Steps 1, 2, and 3 are the **same little dance** with a different file each time. Here it is in
full, slowly:

1. **Plug the Kindle into your computer** with the USB cable. After a moment it shows a "USB
   drive mode" screen and appears on your computer like a USB stick named **Kindle**.
2. **Open that Kindle drive.** The main window you see *is* the "root".
3. **Copy your file for this step into that main window** (the root) — not into any folder.
4. **Safely eject** the Kindle (so the copy finishes), then **unplug** the cable. The Kindle
   goes back to its normal screen.
5. On the **Kindle itself**: press **Home → Menu → Settings → Menu → "Update Your Kindle"**,
   and confirm. The Kindle installs the file and **restarts on its own.**
6. Wait for it to finish restarting (back to the Home screen). That step is done. ✅

> 💡 **Reassurance for the nervous:** while it installs you may see "Your Kindle is
> restarting…" and the screen may go blank or flash for up to a minute. **This is normal.**
> Don't unplug it or press anything during the restart — just let it finish.

If **"Update Your Kindle" is greyed out and you can't tap it**, that means the file on the
Kindle isn't right for your model — see [If something goes wrong](#-if-something-goes-wrong).
Nothing is broken; you'll just swap in the correct file.

---

## The 8 steps

### Step 1 — Jailbreak (unlock the Kindle)
**What it does:** opens the door so your Kindle can run the helpful apps. **Safe and reversible.**

1. Download and unzip the **[jailbreak file](mirror/niluje/kindle-jailbreak-0.13.N-r18833.tar.xz)**.
   Inside is a folder called `Jailbreak` with lots of `.bin` files.
2. Find **your** file. For most people on modern firmware (3.3 or 3.4.x):
   - **B006:** `Update_jailbreak_0.13.N_k3g_install.bin`
   - **B008:** `Update_jailbreak_0.13.N_k3w_install.bin`
   - **B00A:** `Update_jailbreak_0.13.N_k3gb_install.bin`
   - *(Only if your firmware is 3.0, 3.1, or 3.2:* use the matching file that has
     `-3.0-to-3.2` in its name instead.)*
   - Ignore every file with `uninstall` in the name.
3. Do [the pattern above](#-the-pattern-youll-repeat-read-this-once--steps-1-2-and-3-all-work-this-way) with that one file.

**✅ What success looks like:** the Kindle restarts normally and you're back at the Home
screen. You might catch a quick word like `JailBroken` flash by during the restart — that's
a *good* sign. Afterward, "Update Your Kindle" might appear greyed out — also normal and fine.
*(Want proof it worked? Plug back in: the file you copied will be gone, and a new folder
called `linkjail` will be sitting in the root. That folder is the jailbreak. We confirmed
exactly this on the test device.)*

### Step 2 — MKK (lets the Kindle run the new apps)
**What it does:** installs the kit that lets those custom apps actually run. **Silent — you
won't see a change, and that's expected.**

1. Download and unzip the **[MKK file](mirror/niluje/kindle-mkk-20141129-r18833.tar.xz)**.
2. Find your model's file: `Update_mkk-20141129-k3g-B006_install.bin` (B006), or the `k3w-B008`
   / `k3gb-B00A` version for your model. (Ignore `uninstall` files.)
3. Do [the pattern](#-the-pattern-youll-repeat-read-this-once--steps-1-2-and-3-all-work-this-way) with it.

**✅ What success looks like:** the Kindle restarts normally with **no visible change**. That
is correct — MKK works quietly in the background. You'll know for sure it worked when KUAL
opens at Step 5. *(Proof, if you want it: after restarting, the file you copied is gone from
the root, and the `linkjail` folder is still there.)*

### Step 3 — DevCerts (refresh the expired security certificates)
**What it does:** the previous step's security certificates expired in April 2025. Without
this refresh, the apps would refuse to open. This fixes that. **Also silent.**

1. Download and unzip the **[DevCerts file](mirror/devcerts/DevCerts-20250419-KeyStore.zip)**.
2. Find your model's file. ⚠️ **Careful:** these use a **dash** after "Update", not an
   underscore: `Update-mkk-20250419-k3g-B006_keystore-install.bin` (B006), or the `k3w-B008`
   / `k3gb-B00A` version.
3. Do [the pattern](#-the-pattern-youll-repeat-read-this-once--steps-1-2-and-3-all-work-this-way) with it.

**✅ What success looks like:** restarts normally, again **no visible change**. That's expected.
This is the **last** time you'll use "Update Your Kindle" for a while — the next steps are easier.

### Step 4 — Block Amazon's automatic updates
**What it does:** stops Amazon from one day pushing an update that undoes all your work.
**No installing, no restart** — you just make an empty folder. Easiest step here.

1. Plug the Kindle into your computer (USB drive mode) and open the Kindle drive.
2. In the **root** (main window), create a **new folder**. Name it **exactly**:
   `update.bin.tmp.partial`
   - It must be a **folder**, not a file. The dots are part of the name. Copy-paste the name
     to be safe.
3. Safely eject and unplug. Done.

**✅ What success looks like:** the folder is simply sitting there in the root. That's all —
nothing to install. *(Keep the Kindle's Airplane Mode **on** whenever you're not actively using
WiFi, as extra insurance.)*

### Step 5 — KUAL (the apps menu) — 🎉 this is where you'll SEE it working
**What it does:** adds a little app-launcher to your Kindle. **This is the exciting one** —
when it opens, it proves Steps 1–3 all worked.

> ### ⚠️ The KUAL file must MATCH the certificates from Step 3 — this is the #1 K3 trap
> KUAL is a signed app. Your Kindle will only run it if its signature matches the
> certificates you installed. **These steps install NiLuJe's DevCerts (Step 3), so you must
> use NiLuJe's matching KUAL here.** Use the wrong one and KUAL appears in your book list but
> refuses to open with *"This title is not signed by a registered developer."*
>
> **✅ Use exactly this file:** **[`KUAL-KDK-1.0.azw2`](mirror/niluje/KUAL-KDK-1.0.azw2)** from
> this repo's **`mirror/niluje/`** folder (NiLuJe's 2025 build, ~131.0 KB). **This is the one
> we confirmed works on a real B006 / firmware 3.4.3 Kindle.** It's a single file — no unzipping.
>
> **Two files that look right but FAIL** (don't use these with this guide):
> - The **2022 KUAL** (`~127.8 KB`, from a `KUAL-v2.7.29…` ZIP) — signed with a cert that
>   **expired April 17, 2025**.
> - **KindleModding's KUAL** (`~131.7 KB`, in `mirror/kindlemodding/`) — signed with a
>   *different* set of keys that only work if you used the **Hotfix** instead of DevCerts. Right
>   idea, wrong family for this guide.
>
> Bottom line: **the file in `mirror/niluje/` goes with the DevCerts in `mirror/devcerts/`.**
> Don't mix sources. (And pick the `1.0`, not the `2.0` — `2.0` is for newer Kindles.)

1. Download **[`KUAL-KDK-1.0.azw2`](mirror/niluje/KUAL-KDK-1.0.azw2)** (from `mirror/niluje/` —
   see the warning above). It's a single file — **no unzipping needed.**
2. Plug in the Kindle, and copy that file **into the `documents` folder** on the Kindle.
   ⚠️ This is the one step that does **not** use the root — it goes *inside* `documents`,
   where your books live.
3. Safely eject, unplug. On the Kindle, go to **Home**. You'll see a new "book" in your list
   called **KUAL**. **Open it like a book** (select it, press the center button).

**✅ What success looks like:** instead of a book, a small **menu** opens (you'll see a "KUAL"
heading, maybe a collapsed arrow, and "Quit"). 🎉 That's KUAL working — and it proves your
jailbreak, MKK, and certificates are all good. **The menu looking nearly empty is normal** —
it fills up as you install KOReader in the next steps. This is the big "it's alive" moment.

> ### 😟 If you see "This title is not signed by a registered developer"
> The Kindle can't validate KUAL's signature. Work through these in order — **stop as soon as
> KUAL opens.** (On our device, #1 was the fix.)
>
> 1. **Use the matching KUAL** — the [`KUAL-KDK-1.0.azw2` from `mirror/niluje/`](mirror/niluje/KUAL-KDK-1.0.azw2),
>    **not** an older copy and **not** the one in `mirror/kindlemodding/`. See the warning box
>    above for why. Delete the KUAL file from `documents`, copy this one in, then **restart the
>    Kindle** (hold power ~30 s) and open KUAL again. **This is the most common fix.**
> 2. **Re-do Step 3 (DevCerts) and reboot twice.** On the K3 a `.bin` update sometimes *looks*
>    installed (the file disappears) but didn't fully apply. Re-copy the Step 3 keystore file to
>    the root, run "Update Your Kindle," let it reboot — then hold power to reboot **once more**.
>    Open KUAL again.
> 3. **Check the Kindle's clock.** Certificates are only valid between two dates; a Kindle that
>    sat dead for years can have a wildly wrong clock, making a 2025 cert look "not yet valid."
>    **DIY fix (no computer):** turn Airplane Mode off and connect WiFi to your phone hotspot for
>    a minute so it sets its own date, then reopen KUAL. *(On our device the clock was already
>    correct, so this wasn't our problem — but it is for some.)*
> 4. **Last resort — the modern "Hotfix" path.** A newer community fix installs date-proof
>    certificates: [`Update_hotfix_universal.bin`](mirror/kindlemodding/Update_hotfix_universal.bin).
>    If you go this route, you must also use the **KindleModding** KUAL
>    ([`mirror/kindlemodding/KUAL-KDK-1.0.azw2`](mirror/kindlemodding/KUAL-KDK-1.0.azw2)) — they're
>    the same family. Copy the hotfix to the **root**, "Update Your Kindle," reboot, then use the
>    KindleModding KUAL. *(Well-tested on newer Kindles, only lightly tested on the K3 — try 1–3 first.)*
>
> **Other KUAL problems:** blank screen / crash → Step 2 (MKK) didn't take, redo it. KUAL not in
> your book list at all → the file went to the root instead of `documents`; move it and restart.

### Step 6 — MRPI (lets the menu install bigger apps)
**What it does:** a helper so KUAL can install KOReader next.

1. Download and unzip the **[MRPI file](mirror/niluje/kual-mrinstaller-1.7.N-r18983.tar.xz)**.
   Inside are folders like `extensions` (and maybe `mrpackages`).
2. Plug in the Kindle. Copy those folders into the **root**. If your computer asks whether to
   **merge** with existing folders, say **yes/merge**.
3. Safely eject, unplug. Open **KUAL** again.

**✅ What success looks like:** KUAL now shows new entries (a "Helper" / MRPI option). *(Your
Kindle needs about 220 MB free for the next step; if it's full of books, copy a few off first.)*

### Step 7 — KOReader (your new reading app)
**What it does:** installs the modern reading app that can go online safely and read almost
any book format.

1. Download and unzip the **[KOReader file](mirror/koreader/koreader-kindle-legacy-v2026.03.zip)**.
   ⚠️ The filename **must** contain **`kindle-legacy`** — that's the version made for your older
   Kindle. Inside are `extensions` and `koreader` folders.
2. Plug in, copy both folders into the **root**, **merge** if asked. Safely eject, unplug.
3. Open **KUAL**, choose **KOReader**, then choose **"Start KOReader (no framework)"**.

**✅ What success looks like:** the whole screen changes into a clean file browser that looks
nothing like the normal Kindle. That's KOReader running. Use the page-turn buttons, the arrow
pad to move around, the center button to select, and the keyboard to type.
*(To get back to your normal Kindle later: in KOReader, Menu → Exit/Quit. Your old books are untouched.)*

### Step 8 — Anna's Archive plugin (search & download books on the Kindle)
**What it does:** adds book searching right inside KOReader.

1. Download and unzip the **[Anna's Archive plugin](mirror/annas-koplugin/annas.koplugin-v0.1.8.zip)**.
   You'll get a folder named `annas.koplugin` — **no renaming needed.**
2. Plug in the Kindle. Put that `annas.koplugin` folder **inside** the `koreader` ▸ `plugins`
   folder on the Kindle (so the path is `koreader/plugins/annas.koplugin`).
3. Safely eject, unplug. Open **KOReader** (via KUAL → KOReader → no framework). Look in the
   **Search** menu.

**✅ What success looks like:** "Anna's Archive" appears in the Search menu. Choose it, type a
book title with the keyboard, and results appear to download.
**😟 If searching gives a connection error:** this is the one part we haven't fully confirmed on
this old model yet. If it happens, there's a backup plan (a small library you run at home over
plain web) described in **[guide.html](guide.html)**'s troubleshooting.

---

## 📚 How to actually use it (once set up)

1. Turn on your **phone's hotspot** — it must be **2.4 GHz with WPA2** (older Kindles can't do
   5 GHz or the newest WPA3 security).
2. On the Kindle, turn WiFi on and connect to your hotspot.
3. Open **KUAL → KOReader → Start KOReader (no framework)**.
4. **Search → Anna's Archive →** type a title → choose **EPUB** format (best for this small
   screen) → pick a result → it downloads → open it and read. 🎉

---

## 🆘 If something goes wrong

Don't panic — these old Kindles are tough and recoverable.

- **"Update Your Kindle" is greyed out / won't tap.** You have the wrong file for your model
  (or it didn't copy fully). Plug in, delete the `.bin` from the root, and copy the **correct**
  one for your serial (double-check `k3g` vs `k3gb`). Try again. *No harm done.*
- **The screen seems frozen or stuck on a logo.** Hold the **power switch for ~30 seconds** to
  force a restart. If it still misbehaves, plug into the computer, delete the last `.bin` you
  added from the root, and restart. The Kindle is almost certainly fine.
- **KUAL won't open / says expired.** Redo Step 3 (expired) or Step 2 (blank/crash).
- **WiFi won't connect.** Use 2.4 GHz + WPA2, and a simple hotspot password without unusual symbols.
- **A downloaded book won't open.** Re-download it (the source can be flaky).
- **You want your normal Kindle back.** Settings → Factory Reset returns it to stock. (You'd
  then redo this guide if you want the features back.)
- **Truly stuck?** The Kindle has a USB recovery mode that can restore it even from a bad state
  — see [KindleModding.org](https://kindlemodding.org/). A true permanent brick from this guide
  is effectively impossible.

---

## More detail (optional)

- **[guide.html](guide.html)** — the same guide as a styled web page, with extra troubleshooting.
- **[FIELD-NOTES.md](FIELD-NOTES.md)** — our real-device log: every step as we actually did it,
  what matched the instructions and what didn't.
- **[mirror/](mirror/)** — every file, with checksums (`SHA256SUMS`) so you can confirm a download
  is intact, and notes on where each came from.
- **[research/](research/)** — background reading on the hardware, the TLS problem, and self-hosting.

*This guide is maintained as a living document — it gets more accurate every time someone walks
it on a real device. You're not alone in this.* 💛
