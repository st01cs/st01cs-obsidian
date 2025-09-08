---
title: "Adembc/lazyssh: A terminal-based SSH manager inspired by lazydocker and k9s - Written in go"
author:
  - "[[Github]]"
description: "A terminal-based SSH manager inspired by lazydocker and k9s - Written in go - Adembc/lazyssh"
source: "https://github.com/Adembc/lazyssh"
language:
license:
created:
lastUpdated:
tags:
  - "github"
  - "repository"
categories:
  - "[[Repositories]]"
---
[![lazyssh logo](https://github.com/Adembc/lazyssh/raw/main/docs/logo.png)](https://github.com/Adembc/lazyssh/blob/main/docs/logo.png)

---

Lazyssh is a terminal-based, interactive SSH manager inspired by tools like lazydocker and k9s — but built for managing your fleet of servers directly from your terminal.  
With lazyssh, you can quickly navigate, connect, manage, and transfer files between your local machine and any server defined in your `~/.ssh/config`. No more remembering IP addresses or running long scp commands — just a clean, keyboard-driven UI.

---

## ✨ Features

### Server Management

- 📜 Read & display servers from your `~/.ssh/config` in a scrollable list.
- ➕ Add a new server from the UI by specifying alias, host/IP, username, port, identity file.
- ✏ Edit existing server entries directly from the UI.
- 🗑 Delete server entries safely.
- 📌 Pin / unpin servers to keep favorites at the top.
- 🏓 Ping server to check status.

### Quick Server Navigation

- 🔍 Fuzzy search by alias, IP, or tags.
- 🖥 One‑keypress SSH into the selected server (Enter).
- 🏷 Tag servers (e.g., prod, dev, test) for quick filtering.
- ↕️ Sort by alias or last SSH (toggle + reverse).

### Upcoming

- 📁 Copy files between local and servers with an easy picker UI.
- 📡 Port forwarding (local↔remote) from the UI.
- 🔑 Enhanced Key Management:
- Use default local public key (`~/.ssh/id_ed25519.pub` or `~/.ssh/id_rsa.pub`)
- Paste custom public keys manually
- Generate new keypairs and deploy them
- Automatically append keys to `~/.ssh/authorized_keys` with correct permissions

---

## 🔐 Security Notice

lazyssh does not introduce any new security risks. It is simply a UI/TUI wrapper around your existing `~/.ssh/config` file.

- All SSH connections are executed through your system’s native ssh binary (OpenSSH).
- Private keys, passwords, and credentials are never stored, transmitted, or modified by lazyssh.
- Your existing IdentityFile paths and ssh-agent integrations work exactly as before.
- lazyssh only reads and updates your `~/.ssh/config`. A backup of the file is created automatically before any changes.
- File permissions on your SSH config are preserved to ensure security.

## 📷 Screenshots

### 🚀 Startup

[![App starting splash/loader](https://github.com/Adembc/lazyssh/raw/main/docs/loader.png)](https://github.com/Adembc/lazyssh/blob/main/docs/loader.png)

Clean loading screen when launching the app

---

### 📋 Server Management Dashboard

[![Server list view](https://github.com/Adembc/lazyssh/raw/main/docs/list%20server.png)](https://github.com/Adembc/lazyssh/blob/main/docs/list%20server.png)

Main dashboard displaying all configured servers with status indicators, pinned favorites at the top, and easy navigation

---

### 🔎 Search

[![Fuzzy search servers](https://github.com/Adembc/lazyssh/raw/main/docs/search.png)](https://github.com/Adembc/lazyssh/blob/main/docs/search.png)

Fuzzy search functionality to quickly find servers by name, IP address, or tags

---

### ➕ Add Server

[![Add a new server](https://github.com/Adembc/lazyssh/raw/main/docs/add%20server.png)](https://github.com/Adembc/lazyssh/blob/main/docs/add%20server.png)

User-friendly form interface for adding new SSH connections.

---

### 🔐 Connect to server

[![SSH connection details](https://github.com/Adembc/lazyssh/raw/main/docs/ssh.png)](https://github.com/Adembc/lazyssh/blob/main/docs/ssh.png)

SSH into the selected server

---

## 📦 Installation

### Option 1: Homebrew (macOS)

```
brew install Adembc/homebrew-tap/lazyssh
```

### Option 2: Download Binary from Releases

Download from [GitHub Releases](https://github.com/Adembc/lazyssh/releases). You can use the snippet below to automatically fetch the latest version for your OS/ARCH (Darwin/Linux and amd64/arm64 supported):

```
# Detect latest version
LATEST_TAG=$(curl -fsSL https://api.github.com/repos/Adembc/lazyssh/releases/latest | jq -r .tag_name)
# Download the correct binary for your system
curl -LJO "https://github.com/Adembc/lazyssh/releases/download/${LATEST_TAG}/lazyssh_$(uname)_$(uname -m).tar.gz"
# Extract the binary
tar -xzf lazyssh_$(uname)_$(uname -m).tar.gz
# Move to /usr/local/bin or another directory in your PATH
sudo mv lazyssh /usr/local/bin/
# enjoy!
lazyssh
```

### Option 3: Build from Source

```
# Clone the repository
git clone https://github.com/Adembc/lazyssh.git
cd lazyssh

# Build for macOS
make build
./bin/lazyssh

# Or Run it directly
make run
```

---

## ⌨️ Key Bindings

| Key | Action |
| --- | --- |
| / | Toggle search bar |
| ↑↓/jk | Navigate servers |
| Enter | SSH into selected server |
| c | Copy SSH command to clipboard |
| g | Ping selected server |
| r | Refresh background data |
| a | Add server |
| e | Edit server |
| t | Edit tags |
| d | Delete server |
| p | Pin/Unpin server |
| s | Toggle sort field |
| S | Reverse sort order |
| q | Quit |

Tip: The hint bar at the top of the list shows the most useful shortcuts.

---

## 🤝 Contributing

Contributions are welcome!

- If you spot a bug or have a feature request, please [open an issue](https://github.com/adembc/lazyssh/issues).
- If you'd like to contribute, fork the repo and submit a pull request ❤️.

We love seeing the community make Lazyssh better 🚀

---

## ⭐ Support

If you find Lazyssh useful, please consider giving the repo a **star** ⭐️ and join [stargazers](https://github.com/adembc/lazyssh/stargazers).

☕ You can also support me by [buying me a coffee](https://www.buymeacoffee.com/adembc) ❤️  
[![](https://camo.githubusercontent.com/7b8f7343bfc6e3c65c7901846637b603fd812f1a5f768d8b0572558bde859eb9/68747470733a2f2f63646e2e6275796d6561636f666665652e636f6d2f627574746f6e732f76322f64656661756c742d79656c6c6f772e706e67)](https://buymeacoffee.com/adembc)

---

## 🙏 Acknowledgments

- Built with [tview](https://github.com/rivo/tview) and [tcell](https://github.com/gdamore/tcell).
- Inspired by [k9s](https://github.com/derailed/k9s) and [lazydocker](https://github.com/jesseduffield/lazydocker).