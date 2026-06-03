# bootnext

---

## ✨ What is this?

`bootnext` is a lightweight Bash utility that wraps `efibootmgr` and turns UEFI's hidden **BootNext** feature into something actually pleasant to use.

Instead of:

1. Rebooting your computer
2. Mashing `F8`, `F11`, `F12`, `Esc`, `Del`, or whatever random key your motherboard vendor picked from a hat
3. Missing the timing
4. Rebooting again
5. Finally selecting Windows
6. Questioning your life choices

You can simply run:

```bash
bootnext --boot 0000
```

and your machine will reboot into Windows **exactly once**.

After that?

It automatically returns to your normal boot order.

✅ No firmware changes

✅ No GRUB edits

✅ No bootloader wizardry

✅ No dark rituals involving kernel modules

---

## 🤔 Why?

Because this workflow gets old fast:

> "I just need Windows for five minutes."

Reboot.

Open boot menu.

Select Windows.

Use Windows.

Reboot.

Return to Linux.

Repeat until the heat death of the universe.

With `bootnext`:

```bash
bootnext --boot 0000
```

Done.

Go make coffee.

---

## ⚙️ How does it work?

UEFI firmware includes a special variable called:

```text
BootNext
```

When set, the firmware boots that entry **one time only**.

After the boot completes:

```text
BootNext
```

is automatically cleared by the firmware.

Meaning:

```text
Fedora (default)
      │
      ├── bootnext --boot 0000
      │
      ▼
Windows (one-time boot)
      │
      ▼
Fedora (automatically)
```

No permanent changes.

No surprises.

No "why is my machine always booting Windows now?" moments.

---

# 🌟 Features

* 📋 View all available UEFI boot entries
* 🎯 Save a preferred default target
* 🔄 Reboot once into any boot entry
* 💾 Install system-wide with one command
* 🗑️ Clean uninstall support
* 🎨 Human-friendly output
* ⚡ Tiny and fast
* 🔒 No permanent boot order modifications
* 🐧 Works anywhere `efibootmgr` works

---

# 📦 Installation

Clone the repository:

```bash
git clone https://github.com/dhruvcx-1/bootnext.git
cd bootnext
```

Make it executable:

```bash
chmod +x bootnext
```

Install system-wide:

```bash
./bootnext --install
```

Now you can run:

```bash
bootnext --help
```

from anywhere.

---

# 🚀 Quick Start

List available boot entries:

```bash
bootnext --list
```

Example output:

```text
CURRENT  DEFAULT  ID      NAME
-------  -------  ----    --------------------
▶        ★        0000    Windows Boot Manager
                  0007    Fedora
```

---

Save Windows as your preferred target:

```bash
bootnext --set-default 0000
```

Later, whenever you need it:

```bash
bootnext --default
```

Your machine will reboot into Windows once and then return to normal behavior.

---

# 🎮 Common Use Cases

## Linux + Windows Dual Boot

The most common scenario.

You daily-drive Linux but occasionally need Windows for:

* Gaming
* Adobe software
* Firmware updates
* Vendor utilities
* That one ancient application nobody dares replace

Instead of opening your firmware menu:

```bash
bootnext --boot 0000
```

---

## Gaming

Linux all day.

Windows only when absolutely necessary.

Need:

* Anti-cheat support
* VR software
* GPU vendor tools
* RGB software written by eldritch beings

Just run:

```bash
bootnext --boot 0000
```

and suffer Windows only temporarily.

---

## Homelab & Servers

Need to boot into:

* Fedora
* Ubuntu
* Debian
* PXE
* Rescue environments
* Hypervisor installers

Easy:

```bash
bootnext --list
bootnext --boot 0002
```

No monitor required.

---

## Remote Administration

SSH into a machine:

```bash
ssh server
```

Need the next reboot to land somewhere specific?

```bash
bootnext --boot 0000
```

Done.

No KVM.

No physical access.

No sprinting across the building.

---

## Multi-Boot Enthusiasts

Your boot menu looks like:

```text
Fedora
Arch
Ubuntu
Debian
OpenSUSE
NixOS
Windows
Recovery
Random ISO
Another Random ISO
```

And somehow you're still adding more.

`bootnext` makes hopping between them painless.

---

## Testing Operating Systems

Developers, distro hoppers, and chaos enthusiasts can quickly jump between installations without touching firmware settings.

Perfect for:

* Kernel testing
* Distro reviews
* Driver validation
* Breaking things professionally

---

# 📖 Commands

## Show Available Entries

```bash
bootnext --list
```

Displays all detected UEFI boot entries.

---

## Boot Once

```bash
bootnext --boot 0000
```

Sets `BootNext` and immediately reboots.

---

## Save Default Entry

```bash
bootnext --set-default 0000
```

Stores your preferred target for future use.

---

## Show Saved Default

```bash
bootnext --show-default
```

Displays the currently configured default entry.

---

## Reboot Into Saved Default

```bash
bootnext --default
```

Perfect when you've already configured:

```bash
bootnext --set-default 0000
```

and want a quick shortcut forever after.

---

## Install

```bash
./bootnext --install
```

Creates:

```text
/usr/local/bin/bootnext
```

allowing the command to be used globally.

---

## Uninstall

```bash
bootnext --uninstall
```

Removes the installed symlink.

---

# 🛡️ Safety

`bootnext` does **NOT**:

* Modify GRUB
* Modify systemd-boot
* Modify Windows Boot Manager
* Change permanent boot order
* Install services
* Create startup tasks
* Touch your partitions
* Summon demons

It only sets:

```text
BootNext
```

and reboots.

That's literally the entire trick.

---

# 📋 Requirements

You'll need:

* Linux
* UEFI firmware
* `efibootmgr`
* `sudo` access

Install `efibootmgr`:

### Fedora

```bash
sudo dnf install efibootmgr
```

### Ubuntu / Debian

```bash
sudo apt install efibootmgr
```

### Arch Linux

```bash
sudo pacman -S efibootmgr
```

---

# ❓ Frequently Asked Questions

### Will this permanently boot Windows?

No.

That's the exact problem this tool solves.

It only affects the next boot.

---

### Can this break my bootloader?

No.

It doesn't modify bootloader configuration.

---

### Does it work with Secure Boot?

Yes.

`BootNext` is a firmware feature and works independently of Secure Boot.

---

### Does it work with Fedora?

Absolutely.

---

### Does it work with Ubuntu?

Yep.

---

### Does it work with Arch?

Of course.

---

### Does it work with Debian?

Yes.

---

### Does it work with Gentoo?

If you're running Gentoo, you've probably already read the UEFI specification for fun.

---

### Does it work with NixOS?

Probably.

And if it doesn't, you'll rebuild reality until it does.

---

### Does it require GRUB?

No.

It works at the firmware level.

---

### Does it require systemd?

No.

The firmware doesn't care about your init system drama.

---

# 🎭 Example Workflow

Linux user:

```bash
bootnext --set-default 0000
```

Three weeks later:

```bash
bootnext --default
```

PC:

```text
Rebooting...
```

Windows:

```text
Hello.
```

User:

```text
I regret this already.
```

Five minutes later:

```text
Rebooting...
```

Linux:

```text
Welcome back.
```

Balance has been restored.

---

# ❤️ Why I Built This

Because opening a firmware boot menu every time you need another operating system is annoying.

UEFI already solved this problem years ago with `BootNext`.

Most people just don't know it exists.

`bootnext` simply makes that feature easy, memorable, and pleasant to use.

---

# 📜 License

MIT

Use it.

Fork it.

Improve it.

Package it.

Ship it.

Just don't blame me if your motherboard firmware was written by an overworked intern in 2014 and behaves like a haunted toaster.
