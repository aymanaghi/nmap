# 🔍 Nmap Setup Guide

A beginner-friendly guide to installing and using **Nmap** (Network Mapper) on macOS, Windows, Ubuntu/Debian, Fedora/RHEL, and Arch Linux.

> **What is Nmap?**  
> Nmap is a free, open-source tool used to scan networks and discover hosts, open ports, and services. It's widely used by system administrators, security professionals, and students learning about networking.

---

## 📚 Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [macOS](#-macos)
  - [Windows](#-windows)
  - [Ubuntu / Debian](#-ubuntu--debian)
  - [Fedora / RHEL](#-fedora--rhel)
  - [Arch Linux](#-arch-linux)
- [Verify Installation](#verify-installation)
- [Basic Usage Examples](#basic-usage-examples)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## Prerequisites

Before installing Nmap, make sure you have:

- A computer running one of the supported operating systems
- An internet connection to download the software
- Basic familiarity with opening a terminal (or Command Prompt on Windows)
- Administrator / sudo privileges on your machine

> ⚠️ **Legal Notice:** Only scan networks and devices you own or have explicit permission to scan. Unauthorized scanning may be illegal in your country.

---

## Installation

### 🍎 macOS

There are two ways to install Nmap on macOS. We recommend using **Homebrew** as it's the simplest method.

#### Option 1 — Homebrew (Recommended)

1. **Install Homebrew** if you don't have it yet. Open the **Terminal** app and run:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install Nmap** using Homebrew:

   ```bash
   brew install nmap
   ```

3. Homebrew will handle everything automatically. Once done, move on to [Verify Installation](#verify-installation).

#### Option 2 — Official Installer (.dmg)

1. Go to the official Nmap download page: [https://nmap.org/download.html](https://nmap.org/download.html)
2. Download the latest `.dmg` file under the **Mac OS X** section.
3. Open the downloaded `.dmg` file and follow the on-screen instructions.
4. Once installed, open **Terminal** and proceed to [Verify Installation](#verify-installation).

> 💡 **Tip:** You can open Terminal on macOS by pressing `Cmd + Space` and typing "Terminal".

---

### 🪟 Windows

1. Go to the official Nmap download page: [https://nmap.org/download.html](https://nmap.org/download.html)
2. Under the **Microsoft Windows** section, download the latest **self-installer** (e.g., `nmap-7.x-setup.exe`).
3. Run the installer. When prompted, make sure to check:
   - ✅ **Nmap** (core tool)
   - ✅ **Npcap** (required for Nmap to work on Windows)
4. Follow the rest of the on-screen steps and click **Finish**.
5. Open **Command Prompt** or **PowerShell**:
   - Press `Win + R`, type `cmd`, and press Enter.
6. Proceed to [Verify Installation](#verify-installation).

> 💡 **Tip:** If Windows Defender or your antivirus flags the installer, this is a common false positive. Nmap is safe — you can verify the file hash on the official download page.

---

### 🐧 Ubuntu / Debian

Ubuntu, Debian, Linux Mint, and other Debian-based distros use the `apt` package manager.

1. Open your **Terminal**.
2. Update your package list:

   ```bash
   sudo apt update
   ```

3. Install Nmap:

   ```bash
   sudo apt install nmap -y
   ```

4. That's it! Proceed to [Verify Installation](#verify-installation).

> 💡 **Tip:** `sudo` gives you administrator privileges. You'll be asked for your password — this is normal.

---

### 🎩 Fedora / RHEL

Fedora, RHEL, CentOS Stream, and AlmaLinux use the `dnf` package manager.

1. Open your **Terminal**.
2. Install Nmap:

   ```bash
   sudo dnf install nmap -y
   ```

3. On older CentOS / RHEL systems that use `yum`, run:

   ```bash
   sudo yum install nmap -y
   ```

4. Proceed to [Verify Installation](#verify-installation).

---

### 🏹 Arch Linux

Arch Linux and Manjaro use the `pacman` package manager.

1. Open your **Terminal**.
2. Sync your package database and install Nmap:

   ```bash
   sudo pacman -Sy nmap
   ```

3. Confirm the installation when prompted by typing `y` and pressing Enter.
4. Proceed to [Verify Installation](#verify-installation).

---

## Verify Installation

After installing, confirm that Nmap is working correctly by running:

```bash
nmap --version
```

You should see output similar to:

```
Nmap version 7.95 ( https://nmap.org )
Platform: x86_64-pc-linux-gnu
Compiled with: ...
```

If you see a version number, **you're all set!** 🎉

---

## Basic Usage Examples

Here are some simple commands to get you started. Replace `<target>` with an IP address or hostname you own or have permission to scan.

### 1. Scan a Single Host

```bash
nmap <target>
```

Example:
```bash
nmap 192.168.1.1
```

This performs a basic scan and shows which ports are open.

---

### 2. Scan Your Local Network

```bash
nmap 192.168.1.0/24
```

This scans all 254 devices on a typical home network. Useful for seeing which devices are connected.

---

### 3. Detect the Operating System

```bash
sudo nmap -O <target>
```

Nmap will attempt to guess the operating system of the target device.

---

### 4. Detect Services and Versions

```bash
nmap -sV <target>
```

Shows which services (e.g., HTTP, SSH, FTP) are running on open ports, along with their version numbers.

---

### 5. Scan Specific Ports

```bash
nmap -p 22,80,443 <target>
```

Only scans ports 22 (SSH), 80 (HTTP), and 443 (HTTPS).

---

### 6. Verbose Output (More Details)

```bash
nmap -v <target>
```

The `-v` flag makes Nmap print more information as it scans.

---

### 7. Save Results to a File

```bash
nmap <target> -oN results.txt
```

Saves the scan results to a file called `results.txt` in your current directory.

---

### Quick Reference Table

| Command | Description |
|---|---|
| `nmap <target>` | Basic scan |
| `nmap -sV <target>` | Detect service versions |
| `sudo nmap -O <target>` | Detect OS |
| `nmap -p <ports> <target>` | Scan specific ports |
| `nmap -v <target>` | Verbose output |
| `nmap -oN file.txt <target>` | Save results to file |
| `nmap --help` | Show all options |

---

## Troubleshooting

### ❌ `nmap: command not found`

The system can't find Nmap. Try:
- Re-running the install command.
- Restarting your terminal after installation.
- On macOS with Homebrew, run `brew doctor` to check for issues.

---

### ❌ `Permission denied` or `You requested a scan type which requires root privileges`

Some scans require administrator rights. Prefix your command with `sudo`:

```bash
sudo nmap -O <target>
```

On Windows, right-click Command Prompt and select **Run as Administrator**.

---

### ❌ Nmap is very slow

- Try adding `-T4` to speed things up:
  ```bash
  nmap -T4 <target>
  ```
- Make sure the target host is online and reachable.
- Firewalls on the target can slow down or block scans.

---

### ❌ Windows: `Npcap` related errors

- Make sure **Npcap** was installed during setup.
- Re-run the Nmap installer and ensure the Npcap checkbox is checked.
- You can also install Npcap separately from [https://npcap.com](https://npcap.com).

---

### ❌ `Failed to resolve` or `Host seems down`

- Check that the IP address or hostname is correct.
- Try adding `-Pn` to skip the host discovery step:
  ```bash
  nmap -Pn <target>
  ```

---

## Contributing

Contributions are welcome! If you'd like to improve this guide — fix a typo, add a new distro, or improve an explanation — here's how:

1. **Fork** this repository by clicking the Fork button on GitHub.
2. **Clone** your fork to your local machine:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```
3. **Create a new branch** for your changes:
   ```bash
   git checkout -b my-improvement
   ```
4. **Make your changes** and commit them:
   ```bash
   git add .
   git commit -m "Describe what you changed"
   ```
5. **Push** your branch and open a **Pull Request** on GitHub.

Please keep contributions beginner-friendly and consistent with the tone of this guide.

---

## License

This project is licensed under the **MIT License**.

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

See the full license text at [https://opensource.org/licenses/MIT](https://opensource.org/licenses/MIT).

---

<p align="center">Made with ❤️ for university project · Happy scanning! 🔍</p>



## example 
## Scan Result

Target host was online.  
Detected 1 open TCP port: 5678  
Most scanned ports were closed.

This demonstrates host discovery and basic port enumeration using Nmap.
