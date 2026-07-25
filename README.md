# 🧩 Dual‑Boot Wii‑Linux NGX + Rii Loader
Boot Linux or the Wii interface from the same SD card.

This project provides a complete **dual‑boot setup** for the Nintendo Wii, allowing you to choose between:

- **Wii‑Linux NGX** — a modern Linux PPC environment  
- **Rii Loader** — a Wii channel launcher (Wii Menu, homebrew, apps)

The system is controlled by **Gumboot/MINI**, a lightweight bootloader compatible with BootMii.

---

## 🎯 Purpose

To offer a simple and reliable way to boot either:

- **Linux** for development, experimentation, tools, and advanced features  
- **The Wii interface** via Rii Loader for gaming, homebrew launching, and channel management

---

## 🧩 What is Rii Loader?

**Rii Loader** is a Wii **channel and application loader**.  
It allows you to:

- Boot the **Wii Menu** or a **homebrew app** directly from SD  
- Load **custom channels** (WAD, DOL, ELF)  
- Act as an entry point for **BootMii/MINI**  
- Provide a simple graphical interface to select your OS or app  
- Function as a **second operating system** in a dual‑boot setup

In short: **Rii Loader = Wii Menu + Homebrew Launcher + Boot Manager**.

---

## 📦 SD Card Structure

SD Card
├── /boot/
│   ├── wii-linux-ngx-kernel.bin
│   ├── riiloader.bin
│   ├── gumboot.cfg
│
├── /bootmii/   (if using MINI)
│
└── /mnt/wii-rootfs/
├── bin/
├── etc/
├── usr/
└── ...
Code


---

## 🧱 Recommended Partition Layout

| Partition          | Type   | Content                     |
|--------------------|--------|-----------------------------|
| `/dev/mmcblk0p1`   | FAT32  | Rii Loader + Wii apps       |
| `/dev/mmcblk0p2`   | ext2/3 | Wii‑Linux NGX root filesystem |

---

## ⚙️ Dual‑Boot Configuration (Gumboot)

Create `/boot/gumboot.cfg`:

```ini
timeout=5
default=Wii-Linux NGX
```
[Wii-Linux NGX]
kernel=/boot/wii-linux-ngx-kernel.bin
args=root=/dev/mmcblk0p2 rw console=tty0

[Rii Loader]
kernel=/boot/riiloader.bin
args=boot=/dev/mmcblk0p1

Explanation

    timeout=5 → automatically boots Linux after 5 seconds

    default=Wii-Linux NGX → Linux is the default OS

    root=/dev/mmcblk0p2 → Linux rootfs on ext2/ext3 partition

    riiloader.bin → loads the Wii interface from FAT32

🚀 Quick Installation

    Install Gumboot/MINI into /bootmii/ or /boot/

    Copy:

        wii-linux-ngx-kernel.bin → /boot/

        riiloader.bin → /boot/

        your Linux rootfs → /mnt/wii-rootfs/

    Create gumboot.cfg

    Reboot the Wii

    Select Wii‑Linux NGX or Rii Loader at startup

🖼️ Project Logo

(Insert your Wii‑Linux NGX logo image here)
🧰 Optional Linux Startup Script
bash

#!/bin/bash
echo "Booting Wii-Linux NGX..."
sleep 1
modprobe xwiimote
startx

📄 License

MIT License — free to use and modify.
🔗 Useful Links

    Configure Gumboot for dual‑boot

    Install Rii Loader on SD

    Install Wii‑Linux NGX
