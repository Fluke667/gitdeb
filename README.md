# gitdeb - GitHub .deb Package Manager

A package manager for installing and managing .deb packages from GitHub releases.

## Features

- ✅ Install .deb packages directly from GitHub releases
- ✅ Automatic updates via cron jobs
- ✅ GPG signature verification
- ✅ Dependency checking
- ✅ Backup and rollback system
- ✅ Package locking
- ✅ Multi-language support (English, German)
- ✅ Import/Export package lists
- ✅ Search functionality

## Installation

```bash
# 1. Extract the archive
unzip gitdeb-package.zip
cd gitdeb-package

# 2. Install the script
sudo cp usr/local/bin/gitdeb /usr/local/bin/
sudo chmod +x /usr/local/bin/gitdeb

# 3. Copy configuration files
sudo cp -r etc/gitdeb /etc/

# 4. Initialize gitdeb
sudo gitdeb init

# 5. Check system dependencies
sudo gitdeb check
```

## Quick Start

```bash
# Install a package
sudo gitdeb install vscode

# List installed packages
gitdeb list

# Search for packages
gitdeb search editor

# Upgrade all packages
sudo gitdeb upgrade-all

# Set language to German
sudo gitdeb set-language de

# Enable auto-updates
sudo nano /etc/gitdeb/config.conf
# Set: AUTO_UPDATE_ENABLED="yes"
sudo gitdeb cron enable
```

## Usage

### Package Management
```bash
gitdeb install <package>       # Install a package
gitdeb remove <package>        # Remove a package
gitdeb upgrade <package>       # Upgrade a package
gitdeb upgrade-all             # Upgrade all packages
gitdeb rollback <package>      # Restore previous version
```

### Information
```bash
gitdeb list                    # Show installed packages
gitdeb list-available          # Show available packages
gitdeb show <package>          # Show package details
gitdeb search <term>           # Search for packages
```

### Package Control
```bash
gitdeb lock <package>          # Lock package from updates
gitdeb unlock <package>        # Unlock package
gitdeb export [file]           # Export package list
gitdeb import <file>           # Import package list
```

### Security
```bash
gitdeb gpg-list                # List GPG keys
gitdeb gpg-add <id> [url]      # Import GPG key
gitdeb gpg-remove <id>         # Remove GPG key
```

### System
```bash
gitdeb init                    # Initialize gitdeb
gitdeb check                   # Run system check
gitdeb clean                   # Clean cache
gitdeb clean-backups           # Clean old backups
gitdeb cron enable             # Enable auto-updates
gitdeb set-language <lang>     # Set language (en, de)
```

## Configuration

Main configuration file: `/etc/gitdeb/config.conf`

```ini
# Language
LANGUAGE="en"

# Security
VERIFY_SIGNATURES="yes"
REQUIRE_SIGNATURE="no"

# Auto-Update
AUTO_UPDATE_ENABLED="yes"
AUTO_UPDATE_INTERVAL="weekly"
AUTO_UPDATE_TIME="03:00"

# Backup
BACKUP_ENABLED="yes"
BACKUP_KEEP=3
```

## Adding Custom Packages

Create a new configuration file in `/etc/gitdeb/sources.list.d/`:

```bash
sudo nano /etc/gitdeb/sources.list.d/mypackage.conf
```

```ini
NAME="mypackage"
REPO="username/repository"
ASSET_FILTER=".*amd64\.deb$"
ARCH="amd64"
VERSION="latest"
DESCRIPTION="My Package Description"
MAINTAINER="Your Name"
HOMEPAGE="https://github.com/username/repository"
TAGS="tag1,tag2"
DEPENDENCIES=""
CONFLICTS=""
LOCKED="no"
PRIORITY="50"
GPG_KEY=""
GPG_KEY_URL=""
```

## Directory Structure

```
/etc/gitdeb/
├── config.conf              # Main configuration
├── sources.list.d/          # Package definitions
│   ├── vscode.conf
│   ├── signal-desktop.conf
│   └── brave-browser.conf
├── lang/                    # Language files
│   ├── en.lang
│   └── de.lang
├── installed.db             # Installed packages database
└── trusted.gpg              # GPG keyring

/var/cache/gitdeb/           # Downloaded packages
/var/backups/gitdeb/         # Package backups
/var/log/gitdeb.log          # Log file
```

## Examples

### Install VS Code
```bash
sudo gitdeb install vscode
```

### Install Signal Desktop
```bash
sudo gitdeb install signal-desktop
```

### Export installed packages
```bash
gitdeb export my-packages.txt
```

### Import packages on another system
```bash
sudo gitdeb import my-packages.txt
```

### Lock a package from updates
```bash
sudo gitdeb lock firefox
```

### Enable automatic weekly updates
```bash
sudo nano /etc/gitdeb/config.conf
# Set:
# AUTO_UPDATE_ENABLED="yes"
# AUTO_UPDATE_INTERVAL="weekly"
# AUTO_UPDATE_TIME="03:00"
# AUTO_UPDATE_WEEKDAY="0"

sudo gitdeb cron enable
```

## Requirements

- curl
- jq
- dpkg
- apt
- gpg

Install dependencies:
```bash
sudo apt install curl jq dpkg apt gnupg
```

## License

MIT License

## Author

Created for managing GitHub-hosted .deb packages efficiently.
