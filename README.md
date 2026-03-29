# 🛡️ Metasploit & Metasploitable Mastery Guide

> **⚠️ Legal Disclaimer:** This material is strictly for educational purposes and **authorized penetration testing only**. Never use these techniques on systems you do not own or have explicit written permission to test. Unauthorized access is a criminal offense under the Computer Fraud and Abuse Act (CFAA) and equivalent laws worldwide.

## 📄 Overview

`metasploit-mastery.html` is a self-contained, interactive reference guide for learning and mastering the **Metasploit Framework** alongside **Metasploitable 2**, the intentionally vulnerable target VM. It is designed with a terminal-inspired dark interface and covers everything from initial lab setup through post-exploitation techniques — all in one offline-capable HTML file.

This guide is suited for:

- Security students preparing for certifications (OSCP, CEH, eJPT, CompTIA PenTest+)
- CTF players looking to strengthen their exploitation fundamentals
- Developers and sysadmins who want to understand attacker methodologies
- Security professionals building or refreshing their pen-testing skills

## 📁 File Details

| Property | Value |
|---|---|
| **Filename** | `metasploit-mastery.html` |
| **Type** | Standalone HTML (no server required) |
| **Size** | ~75 KB (single file) |
| **Dependencies** | None — fully self-contained |
| **Internet Required** | Only for Google Fonts (degrades gracefully offline) |
| **Compatibility** | Any modern browser (Chrome, Firefox, Edge, Safari) |

## 🚀 Getting Started

No installation is needed. Simply open the file in any modern web browser:

bash
# macOS
open metasploit-mastery.html

# Linux
xdg-open metasploit-mastery.html

# Windows
start metasploit-mastery.html

Or drag and drop the file directly into your browser window.

## 📚 Content Sections

The guide is organized into **9 navigable sections** accessible via the sticky top navigation bar.

### `01` — Framework Overview

Introduces the Metasploit ecosystem and sets the context for ethical usage.

- What Metasploit is and its history (HD Moore, 2003 → Rapid7)
- Difference between **Metasploit Framework** (free/CLI) and **Metasploit Pro** (commercial/GUI)
- What **Metasploitable 2** is and why it is the ideal sandbox target
- Full **penetration testing lifecycle** — from reconnaissance through reporting, mapped to Metasploit phases
- Ethical usage requirements and legal boundaries

### `02` — Lab Environment Setup

Complete walkthrough for building an isolated, safe hacking lab from scratch.

- Required downloads: Kali Linux, Metasploitable 2, VirtualBox
- Step-by-step **VirtualBox host-only network** configuration to isolate the lab from real networks
- PostgreSQL + `msfdb init` setup for enabling the Metasploit database
- Launching and verifying `msfconsole` with a working database connection
- **Metasploitable 2 default credentials table** for all services (SSH, MySQL, Tomcat, phpMyAdmin, Samba, PostgreSQL, VNC)

### `03` — Framework Architecture

Deep dive into how Metasploit is structured internally.

- **Module types** explained: Exploit, Auxiliary, Payload, Post, Encoder, NOP
- Anatomy of a configured exploit module — all options (RHOSTS, RPORT, LHOST, LPORT, PAYLOAD, TARGET) explained with a visual diagram
- **Payload naming convention** breakdown: `<platform>/<arch>/<type>` with examples
- Difference between `reverse_tcp`, `bind_tcp`, `reverse_https` connections
- **Singles vs Stagers vs Stages** payload architecture
- Exploit **reliability rank table** — from ExcellentRanking down to LowRanking with descriptions and examples

### `04` — Core Commands

Comprehensive `msfconsole` command reference organized by category.

- Help, version, and console navigation
- **Workspace management**: creating, switching, and deleting workspaces to separate engagements
- **Module search syntax**: by name, type, platform, CVE, and rank
- Using modules: `use`, `info`, `show options`, `show payloads`, `show advanced`, `show targets`
- **Setting options**: `set`, `setg` (global), `unset`, `unsetg`
- Running modules: `run`, `exploit`, `exploit -j` (background job), `check`
- **Session management**: list, interact, kill, upgrade shell to Meterpreter
- **Database commands**: `hosts`, `services`, `vulns`, `creds`, `loot`, `db_export`

### `05` — Scanning & Enumeration

Techniques for discovering targets, open ports, running services, and vulnerabilities.

- **`db_nmap` integration** — run Nmap scans with results stored directly in the MSF database
- Common Nmap flag combinations: service version (`-sV`), OS detection (`-O`), all ports (`-p-`), UDP (`-sU`)
- **Complete Metasploitable 2 open ports map** — 16 services with port numbers, versions, and known vulnerabilities
- Key **auxiliary scanner modules** for SMB, SSH, MySQL, PostgreSQL, VNC, HTTP
- SSH brute-force with `auxiliary/scanner/ssh/ssh_login` and wordlists
- MySQL and PostgreSQL enumeration and login scanners

### `06` — Exploitation Techniques

Step-by-step exploitation walkthroughs for six major Metasploitable 2 vulnerabilities. Each exploit entry is expandable and includes a full terminal walkthrough with expected output.

| # | Exploit | Port | CVE | Rank |
|---|---|---|---|---|
| 1 | vsftpd 2.3.4 Backdoor | 21 | CVE-2011-2523 | Excellent |
| 2 | Samba `usermap_script` RCE | 445 | CVE-2007-2447 | Excellent |
| 3 | UnrealIRCd 3.2.8.1 Backdoor | 6667 | CVE-2010-2075 | Excellent |
| 4 | Java RMI Server RCE | 1099 | CVE-2011-3556 | Great |
| 5 | Tomcat Manager WAR Upload | 8180 | Misconfiguration | Excellent |
| 6 | PostgreSQL OS Command Injection | 5432 | Misconfiguration | Excellent |

Each entry covers the vulnerability background, attack mechanism, full MSF module configuration, and the expected shell/session output.

### `07` — Meterpreter Deep Dive

Covers the most powerful Metasploit payload in detail.

- What Meterpreter is: in-memory, encrypted, never touches disk, dynamically extensible
- How to **upgrade a plain shell** to a Meterpreter session (`sessions -u` / `shell_to_meterpreter`)
- Full command reference organized by category:
  - System information (`sysinfo`, `getuid`, `getpid`, `ps`, `migrate`, `env`)
  - Networking (`ifconfig`, `route`, `arp`, `netstat`)
  - File system (`ls`, `cd`, `cat`, `download`, `upload`, `search`, `edit`)
  - Privilege escalation (`getsystem`, `getprivs`)
  - Credential dumping (`hashdump`, `run post/linux/gather/hashdump`)
  - Shell dropping (`shell`, `execute`)
  - Port forwarding and pivoting (`portfwd`, `autoroute`)
  - Session management (`background`, `exit`)
  - Persistence (`sshkey_persistence`, `cron_persistence`)
- **Meterpreter extensions**: Stdapi, Priv, Kiwi (Mimikatz), Sniffer — how to load and use each

### `08` — Post-Exploitation

Techniques for maximizing impact after gaining initial access.

- **Linux privilege escalation** workflow using `post/multi/recon/local_exploit_suggester`
- Running local kernel exploits from MSF suggestions
- **Network pivoting** — the concept and full implementation:
  - Discovering internal subnets from a compromised host
  - Adding routes with `route add` and `post/multi/manage/autoroute`
  - Scanning internal networks through the pivot
  - Setting up a **SOCKS5 proxy** (`auxiliary/server/socks_proxy`) for proxychains compatibility
- Post-exploitation module categories with key modules:
  - Credential harvesting (`hashdump`, `ssh_creds`, `credentials/`)
  - System enumeration (`enum_system`, `enum_network`, `env`)
  - Persistence establishment (`sshkey_persistence`, `cron_persistence`)
  - Lateral movement (`autoroute`, TCP port scanner, SOCKS proxy)

### `09` — Master Cheat Sheet

Quick-reference grids for every phase and task — designed for rapid lookup during an engagement.

- Console navigation shortcuts
- Database operation one-liners
- Module search, configuration, and execution commands
- Meterpreter quick-reference (most-used commands in one view)
- **Metasploitable 2 Quick-Win Map** — port → exploit module → result at a glance
- **msfvenom payload generation** — ready-to-copy commands for Linux ELF, Windows EXE, PHP shell, JSP, WAR, with matching `multi/handler` listener setup

## 🔧 Technical Specifications

### Interface Features

- **9-section tabbed navigation** with sticky header — no page reloads
- **Expandable exploit cards** — click any exploit header to reveal the full walkthrough
- Terminal-accurate syntax highlighting with color-coded roles:
  - `green` — prompt characters and success output
  - `yellow` — commands and important values
  - `blue` — informational output and IPs
  - `red` — CVE IDs and error-class output
  - `purple` — module paths
  - `dim` — comments and secondary output
- CRT scanline overlay effect for authentic terminal atmosphere
- Animated warning badge, blinking status indicators, and gradient glow borders
- Fully responsive layout — readable on desktop, tablet, and mobile

### Fonts Used

| Font | Usage | Source |
|---|---|---|
| Orbitron | Display headings | Google Fonts |
| Rajdhani | Body text and UI | Google Fonts |
| Share Tech Mono | Terminal blocks and code | Google Fonts |

## 🧪 Lab Environment Reference

### Recommended Setup
┌─────────────────────────────────────────────────────┐
│                   VirtualBox Host                    │
│                                                     │
│  ┌──────────────────┐    Host-Only    ┌───────────────────────┐
│  │   Kali Linux     │◄──vboxnet0─────►│  Metasploitable 2    │
│  │  192.168.56.101  │   192.168.56.0  │  192.168.56.102      │
│  │  (Attacker)      │                 │  (Target)            │
│  └────────┬─────────┘                 └───────────────────────┘
│           │ NAT (internet for updates)
│           ▼
│      Real Network
└─────────────────────────────────────────────────────┘

### Key IP Addresses (Adjust to Your Lab)

| Role | Host | Default IP |
|---|---|---|
| Attacker | Kali Linux | `192.168.56.101` |
| Target | Metasploitable 2 | `192.168.56.102` |
| Listener | Kali (LHOST) | `192.168.56.101` |
| Listener Port | LPORT | `4444` |

## 📦 Dependencies & Versions Covered

| Tool | Version | Notes |
|------|---------|-------|
| Metasploit Framework | 6.x | All examples tested on MSF6 |
| Metasploitable | 2 (primary), 3 (mentioned) | Ubuntu 8.04-based |
| Kali Linux | 2023.x+ | Recommended attacker OS |
| PostgreSQL | 12+ | Required for database features |
| VirtualBox | 7.x | Recommended hypervisor |
| Nmap | 7.x | Used via `db_nmap` integration |
| msfvenom | Bundled with MSF | Payload generation section |

## 🗺️ Suggested Learning Path

Follow this sequence to build skills progressively:

1. Read Section 01 (Overview)
      ↓
2. Complete Section 02 (Lab Setup) — get your VMs running and pinging each other
      ↓
3. Study Section 03 (Architecture) — understand module types before touching exploits
      ↓
4. Practice Section 04 (Core Commands) — run every command in msfconsole
      ↓
5. Run Section 05 (Scanning) — scan Metasploitable 2 with db_nmap, study the results
      ↓
6. Work Section 06 (Exploitation) — try each exploit one at a time, understand each step
      ↓
7. Master Section 07 (Meterpreter) — spend time with every command category
      ↓
8. Practice Section 08 (Post-Exploitation) — escalate, pivot, persist
      ↓
9. Use Section 09 (Cheat Sheet) as a reference during all CTF and lab work
      ↓
10. Move to HackTheBox / TryHackMe / VulnHub for real-world practice

## 🎯 Next Steps After This Guide

Once comfortable with Metasploitable 2, progress to:

- **TryHackMe** — guided beginner-to-intermediate rooms ([tryhackme.com](https://tryhackme.com))
- **HackTheBox** — intermediate/advanced machines and challenges ([hackthebox.com](https://hackthebox.com))
- **VulnHub** — downloadable intentionally vulnerable VMs ([vulnhub.com](https://vulnhub.com))
- **OffSec PEN-200** — official OSCP course covering advanced Metasploit usage
- **eJPT by eLearnSecurity** — entry-level certification with heavy Metasploit focus

### Complementary Tools to Learn Alongside Metasploit

| Tool | Purpose |
|------|---------|
| Nmap | Network discovery and port scanning |
| Burp Suite | Web application testing |
| Wireshark | Packet analysis |
| John the Ripper / Hashcat | Password cracking |
| Netcat | Raw TCP/UDP connections |
| Hydra | Network brute-forcing |
| LinPEAS / WinPEAS | Automated privilege escalation enumeration |

## ⚠️ Ethical & Legal Notice

This guide and all techniques described herein must only be used:

- On systems you personally own
- On systems where you have **explicit, written authorization** from the owner
- In isolated lab environments (as described in Section 02)
- In the context of approved CTF competitions or training platforms

**Do not** use any technique in this guide against production systems, cloud services, corporate networks, government infrastructure, or any system without documented authorization. The authors accept no liability for misuse of this material.

## 📜 License

This educational material is provided for personal learning and authorized security testing only. Redistribution for commercial purposes without attribution is not permitted.

---

*Built for the security community — learn responsibly, test ethically.*
