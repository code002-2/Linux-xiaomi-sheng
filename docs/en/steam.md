# Steam installation guide (native ARM64)

[中文](../steam.md) | **English**

This guide explains how to install the native ARM64 Steam client manually on the Xiaomi Pad 6S Pro running Linux.
Thanks to Valve's Proton 11 Beta, Steam now has official-grade support on ARM64 Linux; light games run quite well on the Snapdragon 8 Gen 2.

> ⚠️ **Note**: this approach is still experimental and may be unstable. Use it at your own risk.

---

## 📋 Installation

### 1. Download and extract the client

Open a terminal and download the official ARM64 binary package:

```bash
wget https://client-update.steamstatic.com/bins_linuxarm64_linuxarm64.zip.f523fa87fc6b9b5435a5e7370cb0d664ef53b50b
```

Rename and extract it:

```bash
mv bins_linuxarm64_linuxarm64.zip.f523fa87fc6b9b5435a5e7370cb0d664ef53b50b bins_linuxarm64_linuxarm64.zip
unzip bins_linuxarm64_linuxarm64.zip
```

### 2. Move it into the Steam directory

Move the extracted `steamrtarm64` folder into the Steam directory:

```bash
mkdir -p ~/.local/share/Steam
mv steamrtarm64 ~/.local/share/Steam/
```

### 3. Enable the Public Beta

Create the beta configuration file containing `publicbeta`:

```bash
mkdir -p ~/.local/share/Steam/package
echo "publicbeta" > ~/.local/share/Steam/package/beta
```

### 4. Fix permissions

Make sure the Steam directory is readable, writable and executable:

```bash
chmod -R u+rwx ~/.local/share/Steam/steamrtarm64/
```

### 5. Create the library symlink

Some systems lack a specific libvpx version; create a symlink to satisfy the dependency:

```bash
sudo ln -s /usr/lib/aarch64-linux-gnu/libvpx.so.9 /usr/lib/aarch64-linux-gnu/libvpx.so.6
```

If the file already exists, remove the old link first: `sudo rm /usr/lib/aarch64-linux-gnu/libvpx.so.6`

### 6. Start Steam

Enter the client directory and start Steam:

```bash
cd ~/.local/share/Steam/steamrtarm64/
./steam
```

Steam updates itself on first launch. If it crashes, simply run it again. You will need to sign in to your Steam account to finish initialisation.

---

## 🎮 Extra configuration and game launch notes

### Add Proton and the Steam Linux Runtime

Download the Proton11ARM + SteamLinuxRuntimeARM archives from Releases (if they are not there yet, check again later), extract them and move both folders into:

```bash
~/.local/share/Steam/compatibilitytools.d/
```

Create the directory first if it does not exist:

```bash
mkdir -p ~/.local/share/Steam/compatibilitytools.d/
```

### Create the symlink

Create the symlink needed by the Steam SDK:

```bash
ln -s "$HOME/.local/share/Steam/linuxarm64" "$HOME/.steam/sdkarm64"
```

### Install the SDL libraries

Make sure the SDL multimedia libraries are installed:

```bash
sudo apt install libsdl2-mixer-2.0-0 libsdl2-2.0-0
```

### Restart Steam

When you are done, quit Steam completely (including background processes) and start it again.
