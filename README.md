# OpenOMF for Nintendo Switch (OpenOMF-NX-Modern)

[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20My%20Work-ff5e5b?style=flat&logo=ko-fi&logoColor=white)](https://ko-fi.com/thorhax)
[![Build Status](https://img.shields.io/badge/devkitPro-devkitA64%20r29.2-32a852.svg)](https://devkitpro.org)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Release](https://img.shields.io/github/v/release/Thorhax/OpenOMF-NX-Modern?include_prereleases&color=blue)](https://github.com/Thorhax/OpenOMF-NX-Modern/releases)

A modern Nintendo Switch port of **OpenOMF** (open-source remake of *One Must Fall: 2097* by Diversions Entertainment), updated and built with devkitPro (`devkitA64`), GCC 15, libnx 4.12+, Mesa/OpenGL, and modern `switch-sdl2`.

---

## Support My Work

If you enjoy playing retro PC classics and arcade fighters on your Nintendo Switch, consider supporting my work on Ko-fi:

[![Support on Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/thorhax)

Your support helps me maintain, update, and improve homebrew ports for the Nintendo Switch!

---

## 📦 Installation Instructions

### Quick Install (Pre-packaged Zip)
1. Download `openomf-switch-v0.8.7.zip` from the [Releases](https://github.com/Thorhax/OpenOMF-NX-Modern/releases) section.
2. Extract the `openomf` folder directly into `/switch/` on your SD card so that the executable path is `/switch/openomf/openomf.nro`.
3. Ensure the game resource files (`*.DAT`, `*.BK`, `*.AF`, etc.) are located in `/switch/openomf/resources/` (included in the zip release).
4. Launch via the Homebrew Menu (Title Override mode recommended).

### Standalone NRO
1. Download `openomf.nro` from the [Releases](https://github.com/Thorhax/OpenOMF-NX-Modern/releases) section.
2. Place `openomf.nro` at `sdmc:/switch/openomf/openomf.nro`.
3. Copy the original OMF 2097 resource files into `sdmc:/switch/openomf/resources/`.

---

## 🎮 Controls

The controls are mapped to provide a familiar fighting game experience on Joy-Cons and Pro Controllers:

| Action | Controller Mapping |
| :--- | :--- |
| **Punch** | **Y** and **B** |
| **Kick** | **X** and **A** |
| **Movement / Direction** | **D-Pad** & **Left Analog Stick** |
| **Menu / Pause / Exit** | **Plus (+)** |
| **Options / In-Game Menu** | **Minus (-)** |

---

## 🛠 Modernization & Port Details

- **devkitPro / devkitA64 Toolchain Support**: Built against modern devkitA64 toolchains (GCC 15.2.0, libnx 4.12.0).
- **Mesa OpenGL Pipeline**: Uses `switch-mesa` and `switch-glad` with customized GLSL shaders.
- **Embedded RomFS**: Shaders, default configurations, language string tables (`ENGLISH.DAT2`), and game controller databases are embedded directly into the NRO.
- **Fixed Stage Hazard Graphics**: Resolved shader remap calculations and sentinel dimension handling for background hazard animations (e.g. fighter jet bullet impacts in Desert Arena).
- **Audio & Sound**: High-quality music and SFX playback powered by `switch-sdl2_mixer`, `switch-opusfile`, and vendored `libxmp`.
- **Clean Native Execution**: Disabled unbuffered debug logging to SD card to prevent performance bottlenecks.

---

## 🔨 Building from Source

### Prerequisites
- [devkitPro / devkitA64](https://devkitpro.org/wiki/Getting_Started) with `switch-dev`
- Portlibs:
  ```bash
  sudo dkp-pacman -Syu switch-dev switch-sdl2 switch-sdl2_mixer switch-mesa switch-glad switch-enet switch-libpng switch-zlib switch-opusfile
  ```

### Compiling with Docker
```bash
docker run --rm -v $(pwd):/src -w /src devkitpro/devkita64:latest bash -c \
  "cmake -B build-switch -DCMAKE_TOOLCHAIN_FILE=/opt/devkitpro/cmake/Switch.cmake \
   -DCMAKE_BUILD_TYPE=Release -DUSE_MESA=ON && cmake --build build-switch -j$(nproc)"
```

---

## 📜 Credits & License

- Original game by **Diversions Entertainment** and published by **Epic MegaGames** (1994).
- Open-source engine by the [OpenOMF Team](https://github.com/omf2097/openomf).
- Nintendo Switch port & modernizations by **Thorhax**.
- Licensed under the [MIT License](LICENSE).
