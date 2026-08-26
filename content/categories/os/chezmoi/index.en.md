---
title: "Chezmoi: Elegant Dotfile Management Across Linux and Windows"
description: "How to securely and conveniently synchronize user configuration files across different operating systems using chezmoi, Go templates, and Git."
date: 2026-02-25
draft: false
slug: "chezmoi-dotfiles-management"
categories:
  - DevOps
  - Infrastructure
  - OS
tags:
  - Linux
  - Windows
  - Chezmoi
  - Git
  - CLI
---

Managing configuration files (`dotfiles`) across multiple machines inevitably turns into chaos over time. A standard Git repository in your home directory quickly gets cluttered, symlinks often break on Windows, and storing secrets like API tokens or plain-text usernames publicly is extremely unsafe.

The solution to this problem is **chezmoi** — a modern, Go-based dotfile manager. It allows you to manage settings across Linux, WSL, and Windows securely and systematically.

---

### 🚀 Why Choose Chezmoi?

Unlike traditional symlink-based approaches, **chezmoi** stores target configurations in a dedicated directory (by default `~/.local/share/chezmoi`) and applies changes to your live system only when explicitly instructed.

* **Cross-Platform**: Works seamlessly on Unix-like systems, WSL, and Windows.
* **Go Template Support**: Dynamically substitutes variables (such as username, hostname, or email) based on the target host.
* **Built-in Security**: Native encryption support for sensitive data using `age` or `GnuPG`.
* **Automated Provisioning**: Supports `run_once_` scripts to install packages during initial system setup.

---

### 📦 Repository Layout and Structure

Here is an example structure of a chezmoi-managed dotfile repository:

```text
dotfiles/
├── .chezmoi.toml.tmpl                     # Chezmoi configuration template
├── .chezmoiignore                         # Files and directories to ignore
├── dot_bashrc                             # Becomes ~/.bashrc
├── dot_gitconfig.tmpl                     # Template for ~/.gitconfig with variables
├── private_dot_config/                    # Becomes ~/.config/
│   ├── helix/                             # Helix editor configuration
│   ├── starship/                          # Starship prompt setup
│   └── wezterm/                           # Cross-platform WezTerm terminal
├── run_once_after_10-base-packages.sh.tmpl   # Base CLI package installer (Linux/WSL)
└── run_once_after_20-windows-packages.ps1.tmpl # Package installer (Windows)
```

> [!note] Naming Conventions
> Prefixes in chezmoi filenames define their target attributes: `dot_` transforms into a leading dot (`.bashrc`), `private_` creates a restricted folder (`chmod 700`), and `.tmpl` enables the Go template engine.

---

### ⚡ Quickstart and Initialization

#### Linux / WSL

1. **Install the utility:**
   ```bash
   sh -c "$(curl -fsLS get.chezmoi.io)" -- -b ~/.local/bin
   export PATH="$HOME/.local/bin:$PATH"
   ```

2. **Initialize from a GitHub repository:**
   ```bash
   chezmoi init --apply <your-username>
   ```

#### Windows

On Windows, the easiest way to install chezmoi is via the **Scoop** package manager:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
iwr -useb get.scoop.sh | iex
scoop install main/chezmoi git gh

# Initialize configuration inside Git Bash:
chezmoi init --apply <your-username>
```

---

### 🔄 Daily Command Cheatsheet

| Command | Description |
| :--- | :--- |
| `chezmoi edit ~/.bashrc` | Open a file in your default editor. |
| `chezmoi diff` | Show differences between repository state and `$HOME`. |
| `chezmoi apply -v` | Apply changes from source state to the living system. |
| `chezmoi update` | Pull changes from Git repository and apply them immediately. |
| `chezmoi add ~/.config/helix/` | Add a new directory under chezmoi tracking. |
| `chezmoi cd` | Navigate into chezmoi's local source directory. |

---

### 📊 Leveraging Templates

Go templates allow you to maintain a single `dot_gitconfig.tmpl` across all your devices:

```text
[user]
    name = {{ .name }}
    email = {{ .email }}
```

Variables are read from your personal `.chezmoi.toml` file or requested via interactive prompts during initialization.

> [!warning] Caution with Provisioning Scripts
> Scripts prefixed with `run_once_` execute automatically only once. Always verify generated script output prior to running using `chezmoi execute-template < <file>`.
>
> On Windows systems, to prevent accidental execution of Bash scripts, it is recommended to apply changes using:
> `chezmoi apply --exclude=scripts`.

---

### 📚 Resources and Links

* 🌐 [Official Chezmoi Documentation](https://www.chezmoi.io/)
* 🛠 [Sample Dotfiles Repository on GitHub](https://github.com/The-Old-Cat/dotfiles)
