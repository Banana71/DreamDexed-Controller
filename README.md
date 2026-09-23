# DreamDexed Controller

A browser-based controller for **DreamDexed** — the Raspberry Pi port of
**MiniDexed**, a faithful software emulation of the legendary Yamaha DX7.
It gives a headless Raspberry Pi 4 a proper user interface: select
performances, adjust volume, step through banks and programs, and forward
incoming MIDI notes to the Pi — all from a single HTML file.

No extra software. No bridge. No server. The browser talks directly to the
Pi over the Web MIDI API.

A companion **starter page** (`index.html`) walks first-time users through
setup, parts and the first steps.

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

- **MIDI Out** – the Pi itself. Used for Program Change, Bank Select, Volume and the PGM / BANK navigation keys (default channel 10).
- **MIDI In** – your keyboard or DAW. Incoming notes are forwarded 1:1 to the Pi, on their original channel (typically 1). Active Sensing (`0xFE`) is filtered out.
- **PERFLIST.PDF** – opens the Soundplantage Performance List alongside the Controller.
- **MANUAL** – opens the in-app user manual.

The two MIDI channels are kept separate on purpose: notes arrive on channel
1, program changes go out on channel 10 (`PerformanceSelectChannel=10`). This
avoids "ghost notes" — note messages being misinterpreted as program changes.

---

## Requirements

- Raspberry Pi 4 (1 GB is enough)
- USB-C to USB-A cable
- SD card, 8 GB or larger
- PC with Chrome, Edge or Brave
- MIDI keyboard or controller (sends on channel 1)
- Headphones or speakers

A DAC, OLED display or rotary encoder are optional — see section 08 of the
starter page.

> **Warning:** In USB Gadget Mode the Pi is powered through the same USB-C
> cable that carries the data. Do **not** connect a separate power supply.
> See the starter page for details.

---

## Quick start

1. Download DreamDexed from the [DreamDexed releases page](https://github.com/DreamDexed/DreamDexed/releases).
2. Flash the ZIP to the SD card (Raspberry Pi Imager or balenaEtcher).
3. Replace the `minidexed.ini` on the SD card with the one from this repository.
4. Insert the SD card into the Pi and connect it to your PC via USB-C.
5. Open `index.html` (or the hosted URL), then click **Go to Controller**.
6. In the Controller, select the Pi under **MIDI OUT** and press **CONNECT**.
7. Select your keyboard under **MIDI IN**.
8. Enter a performance number and press **ENTER** — then play.

Full instructions, troubleshooting and next steps are on the starter page.

---

## Deploying to GitHub Pages

1. Push all files to the `main` branch.
2. Go to **Settings → Pages**.
3. Set *Source* to `Deploy from a branch`, *Branch* to `main` / `root`.
4. Save. The site will be available at `https://<username>.github.io/<repo>/`.

Rename `start.html` to `index.html` so it becomes the default landing page.

---

## Credits and license

Based on **MiniDexed** by probonopd, licensed under the
[GPL](https://github.com/probonopd/MiniDexed/blob/main/COPYING).

- MiniDexed: https://github.com/probonopd/MiniDexed
- DreamDexed: https://github.com/DreamDexed/DreamDexed
- Performance List and Controller: SOUNDPLANTAGE.COM

The `doto-latin-900-normal.woff2` font is **Doto** by Óliver Lalan, licensed
under the SIL Open Font License.
