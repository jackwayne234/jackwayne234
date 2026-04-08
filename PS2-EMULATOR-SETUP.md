# PS2 Emulator Setup: EverQuest Online Adventures Frontiers on the AYN Thor

Guide for setting up **EverQuest Online Adventures: Frontiers (USA)** [SLUS-20744] on the **AYN Thor** Android handheld using **NetherSX2 Classic** with online play on the **Sandstorm** private server.

---

## Table of Contents

1. [What You Need](#what-you-need)
2. [Install NetherSX2 Classic](#install-nethersx2-classic)
3. [Add PS2 BIOS](#add-ps2-bios)
4. [Prepare the Game ISO](#prepare-the-game-iso)
5. [Configure the Emulator](#configure-the-emulator)
6. [DNAS Bypass (Required for Online Play)](#dnas-bypass-required-for-online-play)
7. [DEV9 Networking Setup](#dev9-networking-setup)
8. [Memory Card Setup](#memory-card-setup)
9. [Connect to Sandstorm Server](#connect-to-sandstorm-server)
10. [Recommended Performance Settings for AYN Thor](#recommended-performance-settings-for-ayn-thor)
11. [Troubleshooting](#troubleshooting)
12. [Resources](#resources)

---

## What You Need

| Item | Details |
|------|---------|
| **Device** | AYN Thor (Snapdragon 8 Gen 2 — Base, Pro, or Max) |
| **Emulator** | NetherSX2 Classic v2.2n or newer (with DEV9 networking support) |
| **PS2 BIOS** | Dumped from your own PlayStation 2 console |
| **Game ISO** | EverQuest Online Adventures: Frontiers (USA) [SLUS-20744] — ripped from your own disc |
| **Wi-Fi** | Required for online play on the Sandstorm server |
| **Storage** | At least 5 GB free (BIOS + ISO + emulator data) |

> **Legal note:** You must dump the PS2 BIOS from your own console and rip the game ISO from your own physical disc. Downloading BIOS files or game ISOs you don't own is piracy.

---

## Install NetherSX2 Classic

NetherSX2 Classic is the recommended PS2 emulator for Android with online multiplayer support (DEV9 Ethernet emulation).

### Option A: Install via Obtainium (Recommended)

1. Install [Obtainium](https://github.com/ImranR98/Obtainium) on your AYN Thor
2. Add the NetherSX2 Classic source: `https://github.com/Trixarian/NetherSX2-classic`
3. Obtainium will download the latest release and notify you of future updates

### Option B: Manual Install

1. Go to [NetherSX2 Classic Releases](https://github.com/Trixarian/NetherSX2-classic/releases)
2. Download the latest `.apk` file
3. If you already have AetherSX2 installed, NetherSX2 Classic is distributed as an xdelta patch — use [UniPatcher](https://play.google.com/store/apps/details?id=org.emunix.unipatcher) on Android to apply the patch to your existing AetherSX2 APK
4. Enable "Install from unknown sources" in Android settings if prompted
5. Install the APK

---

## Add PS2 BIOS

1. Create a folder on your AYN Thor's internal storage: `Internal Storage/NetherSX2/bios/`
2. Copy your PS2 BIOS files into that folder (you need at least one, e.g., `SCPH-70012.bin`)
3. Open NetherSX2 Classic → **Settings** → **BIOS** → select your BIOS file

> A USA-region BIOS (SCPH-30001, SCPH-39001, SCPH-50001, SCPH-70012, etc.) is recommended since EQOA Frontiers is a USA title.

---

## Prepare the Game ISO

1. Rip your physical EverQuest Online Adventures: Frontiers disc to an ISO file using a PC with a DVD drive (tools like ImgBurn work well)
2. Optionally convert the ISO to **CHD format** using [CHDroid](https://play.google.com/store/apps/details?id=org.nicholasgasior.chdroid) to save storage space
3. Transfer the ISO/CHD file to your AYN Thor (e.g., `Internal Storage/PS2/Games/`)
4. In NetherSX2, add the game folder to your library by going to **Settings** → **Game List** → **Game Directories** and adding the path

### Game Identification

- **Title:** EverQuest Online Adventures: Frontiers
- **Region:** USA (NTSC-U)
- **Serial:** SLUS-20744
- **CRC:** `eeee1fcc`

---

## Configure the Emulator

Open NetherSX2 Classic and apply these baseline settings:

### System Settings

- **BIOS:** Your USA-region BIOS
- **Enable Cheats/Patches:** **ON** (required for DNAS bypass)
- **Fast Boot:** ON (skip the PS2 logo — faster startup)

### Graphics Settings (GS)

The AYN Thor's Snapdragon 8 Gen 2 handles PS2 emulation at high resolution. Start with:

- **Renderer:** Vulkan
- **Internal Resolution:** 3x Native (1536x1120) — the Thor handles this comfortably; you can try 4x
- **Texture Filtering:** Bilinear (PS2)
- **Anisotropic Filtering:** 4x or 8x
- **Mipmapping:** Automatic
- **CRC Hack Level:** Automatic

### Emulation Settings (EE/VU)

- **EE Cycle Rate:** 100% (default)
- **EE Cycle Skip:** 0 (disabled)
- **Enable MTVU:** ON (multi-threaded VU — improves performance on multi-core)
- **Clamping Mode:** Normal for both EE and VU

---

## DNAS Bypass (Required for Online Play)

DNAS (Dynamic Network Authentication System) was Sony's online authentication service for PS2. Since Sony shut it down, you need a bypass patch to connect to any server.

### Create the PNACH File

1. On your AYN Thor, navigate to: `Internal Storage/NetherSX2/cheats/` (create the `cheats` folder if it doesn't exist)
2. Create a new text file named: **`eeee1fcc.pnach`** (this is the CRC for EQOA Frontiers USA)
3. Download the correct pnach file from [eqoa.live](https://eqoa.live/) — the Sandstorm server distributes a combined DNAS bypass + server redirect patch

> **Important:** The Sandstorm pnach file handles both the DNAS bypass AND the server connection redirect. With the latest patch, you do NOT need to manually configure DNS settings — the patch redirects the game directly to the Sandstorm server.

### Verify the Patch is Active

1. Open NetherSX2 Classic → **Settings** → **System** → ensure **Enable Cheats** is **ON**
2. Launch the game — you should see a message in the emulator log confirming the patch loaded
3. If the game gets past the DNAS authentication screen, the bypass is working

---

## DEV9 Networking Setup

NetherSX2 Classic v2.2n+ includes DEV9 Ethernet emulation for online play.

### Enable Networking

1. Open NetherSX2 Classic → **Settings** (or **App Settings** → **Settings**)
2. Scroll to the networking section
3. **Enable DEV9 Ethernet:** ON
4. **API:** Sockets
5. **Device:** Wi-Fi (default — use this for the AYN Thor's wireless connection)

### DNS Configuration

With the **latest Sandstorm pnach file**, DNS settings are handled by the patch itself:

- **DNS1:** Leave on Automatic, or set to any valid DNS (e.g., `1.0.0.0`)
- You do **not** need to manually set DNS to the Sandstorm server IP

If using an **older Sandstorm patch** that doesn't include the server redirect:

- **DNS1:** `5.161.217.188` (Sandstorm server — verify the current IP at [eqoa.live](https://eqoa.live/))

---

## Memory Card Setup

EQOA Frontiers stores network configuration on the PS2 memory card.

### Fresh Start (Recommended for Sandstorm)

1. Use a **blank/empty virtual memory card** with no existing EQOA save data
2. NetherSX2 creates memory cards automatically — the default cards work fine
3. When the game boots, it will prompt you to create new network settings
4. Since the Sandstorm pnach handles the server redirect, you can accept default network settings

### If Prompted for Network Configuration In-Game

- **Connection type:** Select your connection method
- **IP Address:** Automatic (DHCP) is fine
- **DNS:** Automatic (the pnach patch handles redirection)
- **Gateway:** Leave as default

---

## Connect to Sandstorm Server

1. Ensure your AYN Thor is connected to Wi-Fi
2. Launch EQOA Frontiers in NetherSX2 Classic
3. The game will attempt DNAS authentication — the bypass patch skips this
4. At the server selection screen, you should see the **Sandstorm** server
5. Connect and create your character

### First-Time Setup

- Create an account on the [Sandstorm server](https://eqoa.live/) if required (check their site for current registration process)
- Join the [Sandstorm Discord](https://eqoa.live/) for community support, server status, and patch updates

---

## Recommended Performance Settings for AYN Thor

The AYN Thor with Snapdragon 8 Gen 2 is one of the best handhelds for PS2 emulation. These settings are tuned for EQOA Frontiers:

| Setting | Value | Notes |
|---------|-------|-------|
| **Internal Resolution** | 3x Native | Bump to 4x if performance stays solid |
| **Renderer** | Vulkan | Best GPU performance on Snapdragon |
| **Frame Limit** | 60 FPS (NTSC) | Default for the game |
| **MTVU** | ON | Significant multi-core speedup |
| **EE Cycle Rate** | 100% | Reduce to 75% only if needed |
| **Fast CDVD** | ON | Faster loading for ISO/CHD files |
| **Async Texture Loading** | ON | Smoother texture streaming |

### Controller Mapping

The AYN Thor has a full controller layout (dual analog sticks, D-pad, face buttons, shoulders, triggers). The default mapping should work. Customize in **Settings** → **Controllers** if needed.

EQOA uses:
- **Left stick:** Movement
- **Right stick:** Camera
- **D-pad:** Menu navigation
- **X:** Confirm / Interact
- **O:** Cancel / Back
- **Triangle:** Open menu
- **L1/R1:** Cycle targets
- **L2/R2:** Additional actions

### Using the Bottom Screen

The AYN Thor's bottom touchscreen (3.92") can be mapped to:
- A virtual keyboard (useful for in-game chat in EQOA)
- Quick-access buttons for save states or emulator toggles
- A game guide or map reference

---

## Troubleshooting

### Game won't boot / black screen
- Verify your BIOS is a valid USA-region PS2 BIOS
- Try switching the renderer from Vulkan to OpenGL
- Ensure the ISO is not corrupted (re-rip from disc)

### DNAS authentication fails
- Confirm the `eeee1fcc.pnach` file is in the correct `cheats` folder
- Verify **Enable Cheats** is ON in emulator settings
- Re-download the latest pnach from [eqoa.live](https://eqoa.live/)

### Cannot connect to Sandstorm server
- Check that **DEV9 Ethernet** is enabled and set to **Sockets** mode
- Verify your AYN Thor has an active Wi-Fi connection
- Confirm you're using the latest Sandstorm pnach (it includes the server redirect)
- If using the old patch, verify the DNS IP address is current at [eqoa.live](https://eqoa.live/)
- Check the [Sandstorm Discord](https://eqoa.live/) for server status — it may be down for maintenance

### Slow performance / frame drops
- Lower internal resolution from 3x to 2x Native
- Enable **Fast CDVD**
- Disable **Anisotropic Filtering**
- Close other apps running on the AYN Thor

### Game crashes during play
- Try the **NetherSX2 Classic** build (3668) rather than standard (4248) — Classic tends to be more stable for online games
- Save states are **not compatible** between Classic and Standard builds — always use in-game saves when switching

### In-game chat / keyboard
- Use the AYN Thor's bottom touchscreen for virtual keyboard input
- Alternatively, pair a Bluetooth keyboard for easier chat

---

## Resources

| Resource | Link |
|----------|------|
| **Sandstorm Server (Official)** | [eqoa.live](https://eqoa.live/) |
| **Sandstorm Discord** | Available via [eqoa.live](https://eqoa.live/) |
| **NetherSX2 Classic Releases** | [GitHub — Trixarian/NetherSX2-classic](https://github.com/Trixarian/NetherSX2-classic/releases) |
| **EQOA Frontiers PCSX2 Wiki** | [wiki.pcsx2.net](https://wiki.pcsx2.net/EverQuest_Online_Adventures:_Frontiers) |
| **EQOA Revival Wiki** | [wiki.eqoarevival.com](https://wiki.eqoarevival.com/index.php/Client_Setup) |
| **EQOA Emu Project** | [eqoaemu.com](https://eqoaemu.com/) |
| **Project: Return Home** | [projectreturnhome.com](https://www.projectreturnhome.com/) |
| **Obtainium (App Manager)** | [GitHub — ImranR98/Obtainium](https://github.com/ImranR98/Obtainium) |
| **AYN Thor Setup Guide** | [retrohandhelds.gg](https://retrohandhelds.gg/ayn-thor-setup-guide/) |
| **PS2 Online Gaming Community** | [ps2onlinegaming.com](https://ps2onlinegaming.com/) |

---

*Last updated: April 2026*
