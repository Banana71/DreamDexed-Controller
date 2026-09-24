# DreamDexed Controller for Raspberry Pi 4

A browser-based controller for **DreamDexed / miniDexed**, a faithful software
emulation of the legendary Yamaha DX7.

The Controller lets you select performances, adjust volume, navigate banks
and programs, and forward incoming MIDI notes to the Pi — all from a single
HTML file. No additional hardware is required on the Raspberry Pi. This makes
it easy to try out DreamDexed or miniDexed with nothing more than a Raspberry
Pi 4, and to explore what the instrument can do.

No additional software. No bridge. No server. The browser communicates
directly with the Pi via the Web MIDI API.

A companion start page (`index.html`) guides first-time users through setup,
parts and the first steps.

---

<img width="768" height="735" alt="DreamDexed-Controller" src="https://github.com/user-attachments/assets/86c24072-a8bf-49c9-a69a-965ffeb6bc5c" />

---

## What this repository contains

| File | Purpose |
|------|---------|
| `controller.html` | The Controller — performance selection and MIDI forwarding |
| `index.html` | Starter page — setup guide, parts list, downloads |
| `minidexed.ini` | Pre-configured configuration file for the SD card |
| `doto-latin-900-normal.woff2` | Local font, used by both pages |

---

## How the Controller works

DreamDexed runs headless on a Raspberry Pi 4. In **USB Gadget Mode** the Pi
appears on the PC as a standard MIDI device. The Controller sends MIDI
Program Change and Note messages to it, and forwards incoming MIDI data
from a keyboard or DAW. Everything happens in the browser.

- **MIDI Out** – the Pi itself. Used for Program Change, Bank Select, Volume
  and the PGM / BANK navigation keys (default channel 10).
- **MIDI In** – your keyboard or DAW. Incoming notes are forwarded 1:1 to
  the Pi, on their original channel (typically 1). Active Sensing (`0xFE`)
  is filtered out.
- **PERFLIST.PDF** – opens the modified Performance List that ships with this
repository. Bank 1 is a curated selection of favourites chosen for this
project; Banks 2 and up are the original Soundplantage banks.
- **MANUAL** – opens the in-app user manual.

The two MIDI channels are kept separate on purpose: notes arrive on channel
1, program changes go out on channel 10 (`PerformanceSelectChannel=10`). This
avoids "ghost notes" — note messages being misinterpreted as program changes.

---

## Requirements

- Raspberry Pi 4 (1 GB is enough)
- USB-C to USB-A cable
- SD card, 8 GB or larger
- PC or laptop running **Windows, macOS or Linux**
- **A Chromium-based browser** (Chrome, Edge or Brave)
- **MIDI keyboard or controller** connected to the PC via USB (must be able
  to send on **MIDI channel 1** — all performances are configured to listen
  on channel 1)
- Headphones or speakers

A DAC, OLED display or rotary encoder are optional — see section 08 of the
starter page.

### Browser compatibility

The Controller relies on the **Web MIDI API**, which is not available in all
browsers. The current support:

| Browser | Support |
|---------|---------|
| Chrome / Edge / Brave / Opera (desktop) | **Full support** |
| Firefox (desktop) | Supported from version 108, requires a Site Permission Add-On |
| Safari (macOS / iOS) | **Not supported** |
| Mobile browsers (iOS / Android) | Very limited or no support |

For the most reliable experience, use **Chrome, Edge or Brave** on a desktop
operating system. These browsers provide full Web MIDI support out of the box.

> **Warning:** In USB Gadget Mode the Pi is powered through the same USB-C
> cable that carries the data. Do **not** connect a separate power supply.
> See the starter page for details.

---

## Quick start

1. Download [`Main.zip`](https://github.com/Banana71/DreamDexed-Controller/archive/refs/heads/main.zip) (the whole project).
2. Extract it. You get a folder `DreamDexed-Controller-main/` with the
   Controller, the Install Guide, and a subfolder `SD-Card/` containing the
   ready-to-copy SD-card files.
3. Format an SD card as FAT32 and copy the **contents** of `SD-Card/` to the
   card's root (not the folder itself).
4. Insert the SD card into the Pi and connect it to your PC via USB-C.
5. Open `index.html` (or the hosted URL), then click **Go to Controller**.
6. In the Controller, select the Pi under **MIDI OUT** and press **CONNECT**.
   Connect your **MIDI keyboard** and select it under **MIDI IN**.
7. Enter a performance number and press **ENTER** — then play a note on your
   keyboard.

Full instructions, troubleshooting and next steps are on the install guide page.

---

## Credits and license

Based on **MiniDexed** by probonopd, licensed under the
[GPL](https://github.com/probonopd/MiniDexed/blob/main/COPYING).

- MiniDexed: https://github.com/probonopd/MiniDexed
- DreamDexed: https://github.com/DreamDexed/DreamDexed
- Performance List and Controller: SOUNDPLANTAGE.COM

The `doto-latin-900-normal.woff2` font is **Doto** by Óliver Lalan, licensed
under the SIL Open Font License.
