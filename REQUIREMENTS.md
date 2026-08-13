# Screenpipe Workspace System Requirements & Dependencies

This document details all prerequisites and native toolchain dependencies required to build and run Screenpipe across **Windows**, **macOS**, and **Linux**.

---

## 1. Core Toolchains & Package Managers

| Dependency | Required Version | Install Command (Windows) | Install Command (macOS) | Install Command (Linux / Ubuntu) |
| :--- | :--- | :--- | :--- | :--- |
| **Node / Bun** | `bun >= 1.1` | `winget install Oven-sh.Bun` | `brew install bun` | `curl -fsSL https://bun.sh/install \| bash` |
| **Rust Toolchain** | `rustc >= 1.80` | `winget install Rustlang.Rustup` | `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs \| sh` | `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs \| sh` |
| **FFmpeg** | `ffmpeg >= 6.0` | `winget install Gyan.FFmpeg` | `brew install ffmpeg` | `sudo apt update && sudo apt install -y ffmpeg` |
| **Git** | `git >= 2.40` | `winget install Git.Git` | `brew install git` | `sudo apt install -y git` |

---

## 2. Platform-Specific Native C/C++ Libraries

### **A. Windows (x86_64)**
1. **Visual Studio C++ Build Tools 2022** (Desktop development with C++ workload, MSVC v143, Win 10/11 UCRT SDK).
2. **MSYS2 / MinGW64 Clang:** `winget install MSYS2.MSYS2` then inside MinGW shell: `pacman -S mingw-w64-x86_64-clang`.
3. **Environment Variables:**
   - `LIBCLANG_PATH="C:\msys64\mingw64\bin"`
   - `BINDGEN_EXTRA_CLANG_ARGS='--target=x86_64-pc-windows-msvc ...'`

### **B. macOS (Apple Silicon / Intel)**
1. **Xcode Command Line Tools:** `xcode-select --install`
2. **CMake:** `brew install cmake` *(Required by `whisper-rs-sys` to build `whisper.cpp`)*
3. **Frameworks:** ScreenCaptureKit, AVFoundation, Metal, CoreGraphics *(Included in macOS SDK)*

### **C. Linux (Ubuntu / Debian)**
```bash
sudo apt update && sudo apt install -y \
  build-essential cmake pkg-config clang libclang-dev \
  libssl-dev libasound2-dev libtesseract-dev tesseract-ocr \
  libx11-dev libxtst-dev libxcb1-dev libxext-dev
```

---

## 3. Quickstart Build Commands

### **A. CLI Engine (`screenpipe.exe`)**
```bash
cargo build --release --bin screenpipe
./target/release/screenpipe record
```

### **B. Desktop App & Web UI**
```bash
cd apps/screenpipe-app-tauri
bun install
bun dev:tauri       # Native Tauri Desktop App
bun dev:web         # Web UI Mock Mode (http://127.0.0.1:1420)
bun dev:web:live    # Web UI Live Mode connected to local engine
```
