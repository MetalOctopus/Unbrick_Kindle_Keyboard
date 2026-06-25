# Field Notes — The Tale of How We Made This Work

This is the chronological, real-device companion to `guide.html`. The guide is the
*clean* 8-step procedure. This file is the **honest log**: what actually happened when
a human + an LLM (Claude Code) sat down with a real Kindle Keyboard and worked through
it, including the hurdles that don't appear in any tidy step list.

**Who this is for:** the next person — almost certainly with an LLM assistant riding
along — doing this on their own device. Where the guide says "connect the Kindle," this
file tells you what "connected" actually looks like, what breaks first, and how we knew
we were on the right track.

**How to read it:** chapters are in the order we hit them. Each records the *setup* we
were in, *what we found*, *the fix*, and *what success looked like* so you can match it
against your own screen/terminal.

---

## Chapter 0 — Getting the Kindle Visible to Your Tools

Before Step 1 of the guide (the jailbreak) can happen, you need to actually read and
write the Kindle's USB drive from wherever your assistant is running. For us that was
**Claude Code inside WSL2 (Ubuntu) on a Windows machine, with the Kindle plugged into
the Windows host over USB.** This is a very likely setup for an LLM-assisted user, so
it's worth documenting in full.

### The setup
- Windows PC, Kindle Keyboard connected by USB micro-B cable.
- Kindle awake and showing **USB Drive Mode** (this is what makes it present as a mass-
  storage drive; if it's just charging/asleep it won't mount).
- The assistant (Claude Code) running in a WSL2 Linux distro on that same machine.

### What we found
- **Windows saw the Kindle immediately.** It assigned it a drive letter (for us, `G:`,
  volume label `Kindle`, type *Removable*). Windows device list also showed a `Kindle`
  (WPD) device and a `Kindle Internal Storage USB Device` — both healthy.
- **WSL did *not* auto-mount it.** WSL2 auto-mounts *fixed* drives (C:, D:, …) under
  `/mnt/<letter>`, but **removable USB drives are not auto-mounted**. The mount point
  `/mnt/g` existed but was empty — easy to misread as "the Kindle isn't there" when it
  actually is.
- The Linux block-device tools (`lsblk`, `/dev/sd*`) **won't** show it either: the
  Kindle is mounted on the Windows host and reaches WSL through the 9p/drvfs layer, not
  as a passed-through USB block device. So don't go looking for `/dev/sdX`.

### How to find your drive letter
Don't assume `G:`. From WSL you can ask Windows directly:

```bash
/mnt/c/Windows/System32/WindowsPowerShell/v1.0/powershell.exe -NoProfile -Command \
  "Get-Volume | Select-Object DriveLetter,FileSystemLabel,DriveType | Format-Table -AutoSize"
```

Look for the row whose label is `Kindle` and type `Removable`. That letter is yours.

### The fix — mount it manually
Mounting a drvfs drive needs root, so this runs with `sudo`:

```bash
sudo mount -t drvfs G: /mnt/g      # replace G: and /mnt/g with your letter
```

If your assistant can't run interactive `sudo` (Claude Code in WSL can't supply a
password non-interactively), run the command yourself. In Claude Code you can type it
with a leading `!` so the assistant sees the result:

```
! sudo mount -t drvfs G: /mnt/g
```

### What success looks like
After mounting, listing the drive shows the Kindle's signature top-level folders:

```bash
ls -a /mnt/g
# expect: documents/  system/  audible/  music/  .active-content-data  (and System Volume Information)
```

If you see those, you can read and write the Kindle's root from your tools, and you're
ready for the guide's Step 1. **The guide's repeated "copy the .bin to the root of the
Kindle" means this mount point** (`/mnt/g` here).

### The passwordless-sudo wrinkle (and a namespace gotcha)
Two things bit us here, both worth knowing:

1. **`sudo mount` needs a password**, which an LLM assistant can't type non-
   interactively. We fixed it once with a tightly-scoped sudoers rule covering *only*
   mount/umount, so the assistant can run the ~7 mount/eject cycles itself:
   ```bash
   echo "$USER ALL=(root) NOPASSWD: /usr/bin/mount, /usr/bin/umount" \
     | sudo tee /etc/sudoers.d/kindle-mount
   ```
   (Mode `0644` is fine — sudo only rejects *world-writable* sudoers files. Verify the
   rule with `sudo -n -l`.)
2. **Mount namespaces.** If you mount the Kindle in one shell (e.g. your interactive
   root shell) but your assistant's tools run in a *different* WSL mount namespace, the
   assistant won't see your mount, and vice-versa. The empty `/mnt/g` is the tell. The
   clean fix is the same rule above: let the assistant mount it **in its own
   namespace** so the thing that needs to read the files is the thing that mounted them.

### Finding your serial prefix and firmware version
The model→`.bin` choice in Step 1 hinges on your serial prefix (B006/B008/B00A), and the
guide covers firmware 3.0–3.4.3. **Neither is on the USB partition** — we searched; the
exposed drive only holds `documents/`, `system/`, `audible/`, `music/`. Both live on the
Kindle's hidden root partition. So read them off the **device screen**, not the files:

> On the Kindle: **Home → Menu → Settings**. The serial number is shown on that screen
> (note the first 4 characters), and the **firmware version is at the very bottom**
> (e.g. `Kindle 3.4.3`).

### What a clean starting device looks like
Confirm you're starting from stock before Step 1: the Kindle root should have **no stray
`.bin` files**, **no `update.bin.tmp.partial` folder**, and `documents/` should contain
only your books — no `KUAL` entries or other homebrew. If you see those, someone's
already been here; adjust accordingly.

> **Status: CONFIRMED on our device.** Kindle = `G:` (removable, not auto-mounted, root
> required); passwordless-sudo rule installed; mount succeeded in the assistant's own
> namespace; read + write to the Kindle root verified; device is clean/un-jailbroken.
> Ready for Step 1. Serial/firmware to be read off the Settings screen next.

### Tip for the road ahead — you'll mount/unmount a LOT
Every guide step that installs a `.bin` follows the same loop: mount → copy file →
**eject** → run "Update Your Kindle" on the device → it reboots → mount again to verify.
You'll do this ~7 times. Two things make it less painful:

- **Ejecting from WSL:** unmount cleanly before you eject on the device side, e.g.
  `sudo umount /mnt/g`, then use the Kindle's on-screen eject / unplug.
- **Skip the password prompts (optional):** if you want the assistant to handle the
  mount/unmount cycle itself, add a passwordless sudo rule for just those two commands
  (e.g. via `visudo`). Your call — it trades a little security for a lot less friction.
