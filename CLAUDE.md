# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Bash shell script project for automated installation and management of Xray-core and sing-box VPN/proxy servers. The main script (`install.sh`) is a comprehensive ~10,000 line shell script that provides one-click installation of various proxy protocols.

## Main Commands

### Script Execution
```bash
# Primary installation and management script
./install.sh

# Alternative downloads:
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/chaslui/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

### Quick Access
After installation, the script creates a shortcut:
```bash
vasma  # Opens the main script menu
```

The script is installed to `/etc/v2ray-agent/install.sh` and symlinked to `/usr/bin/vasma` and `/usr/sbin/vasma`.

### Utility Scripts
- `shell/install_en.sh` - English version of the installer
- `shell/init_tls.sh` - TLS certificate initialization
- `shell/send_email.sh` - Email notifications
- `shell/empty_login_history.sh` - Clear login history
- `shell/ufw_remove.sh` - UFW firewall management

## Architecture

### Core Components
- **Main Script**: `install.sh` (~10,000 lines)
  - System detection and compatibility checks
  - Package management for different Linux distributions (CentOS, Ubuntu, Debian, Alpine)
  - VPN/proxy server installation and configuration
  - Certificate management (automatic Let's Encrypt)
  - Subscription management
  - Multi-protocol support

### Supported Protocols
- VLESS (Reality, Vision/TCP, WS, gRPC, XHTTP)
- VMess (TCP, WS, HTTPUpgrade)  
- Trojan (TCP, gRPC)
- Hysteria2 (sing-box)
- Tuic (sing-box)
- NaiveProxy (sing-box)

### Key Functions
The main script contains hundreds of functions organized by purpose:
- System checking (`checkSystem()`, `checkCPUVendor()`, `checkBTPanel()`)
- Installation management (`readInstallType()`, `readInstallProtocolType()`)
- Configuration management (`readAcmeTLS()`, `readCustomPort()`)
- Firewall management (`allowPort()`, `checkUFWAllowPort()`)
- Network utilities (`getPublicIP()`)

### File Structure
- `/` - Main installation script
- `documents/` - Documentation and guides
- `shell/` - Utility scripts
- `fodder/` - Static assets (images, web templates)

### Platform Support
- CentOS/RHEL (yum-based)
- Ubuntu/Debian (apt-based) 
- **Alpine Linux (apk-based) - Full 3.20+ support with AppArmor**
- Architecture support: amd64, arm64, armv7

### Alpine Linux Enhancements
- **AppArmor Security**: Uses AppArmor instead of SELinux for Alpine systems
- **OpenRC Services**: Native OpenRC service management support  
- **Package Optimization**: Alpine-specific package names (iputils, dcron, etc.)
- **Enhanced Compatibility**: Special handling for Alpine 3.20+ features

## Development Notes

- The script is primarily written in Bash with extensive system compatibility checks
- Uses color-coded output via `echoContent()` function
- Implements comprehensive error handling and user input validation
- Modular function design despite being in a single large file
- No build process required - direct script execution
- Configuration files are managed in `/etc/v2ray-agent/`