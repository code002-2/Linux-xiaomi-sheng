# Steam 手动安装指南（原生 ARM64）

**中文** | [English](en/steam.md)

本指南介绍如何在小米平板 6S Pro 的 Linux 系统上手动安装原生 ARM64 版本的 Steam 客户端。
得益于 Valve 推出的 Proton 11 Beta，Steam 现已在 ARM64 Linux 上获得了官方级别的支持；骁龙 8 Gen 2 平台上轻量级游戏的性能表现相当出色。

> ⚠️ **请注意**：本方案仍处于测试阶段，可能遇到不稳定情况，请自行承担风险。

---

## 📋 安装步骤

### 1. 下载并解压客户端

打开终端，执行以下命令下载官方 ARM64 二进制包：

```bash
wget https://client-update.steamstatic.com/bins_linuxarm64_linuxarm64.zip.f523fa87fc6b9b5435a5e7370cb0d664ef53b50b
```

下载完成后，重命名文件并解压：

```bash
mv bins_linuxarm64_linuxarm64.zip.f523fa87fc6b9b5435a5e7370cb0d664ef53b50b bins_linuxarm64_linuxarm64.zip
unzip bins_linuxarm64_linuxarm64.zip
```

### 2. 放置到 Steam 目录

将解压出的 steamrtarm64 文件夹移动到 Steam 目录下：

```bash
mkdir -p ~/.local/share/Steam
mv steamrtarm64 ~/.local/share/Steam/
```

### 3. 启用 Public Beta

创建 Beta 配置文件，加入 publicbeta：

```bash
mkdir -p ~/.local/share/Steam/package
echo "publicbeta" > ~/.local/share/Steam/package/beta
```

### 4. 调整权限

确保 Steam 目录具有正确的读写执行权限：

```bash
chmod -R u+rwx ~/.local/share/Steam/steamrtarm64/
```

### 5. 创建库文件软链接

某些系统可能缺少特定版本的 libvpx，创建软链接以解决依赖问题：

```bash
sudo ln -s /usr/lib/aarch64-linux-gnu/libvpx.so.9 /usr/lib/aarch64-linux-gnu/libvpx.so.6
```

如果提示文件已存在，请先删除原链接：`sudo rm /usr/lib/aarch64-linux-gnu/libvpx.so.6`

### 6. 启动 Steam

进入客户端目录并启动 Steam：

```bash
cd ~/.local/share/Steam/steamrtarm64/
./steam
```

首次启动时，Steam 会进行更新。如遇到闪退，再次运行即可。首次启动后需要登录 Steam 账户以完成初始化。

---

## 🎮 额外配置与游戏启动经验

### 添加 Proton 与 Steam Linux 运行时

前往 Releases 下载压缩包 Proton11ARM + SteamLinuxRuntimeARM（如果还没看到，稍后再看），解压后将两个文件夹都放入以下目录：

```bash
~/.local/share/Steam/compatibilitytools.d/
```

如果该目录不存在，请先创建：

```bash
mkdir -p ~/.local/share/Steam/compatibilitytools.d/
```

### 创建符号链接

为 Steam SDK 创建必要的软链接：

```bash
ln -s "$HOME/.local/share/Steam/linuxarm64" "$HOME/.steam/sdkarm64"
```

### 安装 SDL 库

确保系统已安装 SDL 多媒体库：

```bash
sudo apt install libsdl2-mixer-2.0-0 libsdl2-2.0-0
```

### 重启 Steam

完成上述步骤后，完全退出 Steam（包括后台进程），然后重新启动。
