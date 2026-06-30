# CTF-Machine
# West-Wild CTF - Modified Edition

## 📋 Overview

This is a modified version of the **West-Wild v1.1** VulnHub CTF machine, customized for a
cybersecurity capture-the-flag assignment. The original machine has been enhanced with
additional users, a professional profile website with hidden credential clues,
steganography challenges, and proper firewall hardening.

| Field | Value |
|---|---|
| **Base Machine** | West-Wild v1.1 by Hashim Alsharef |
| **Original Source** | https://www.vulnhub.com/entry/westwild-11,338/ |
| **Difficulty** | Intermediate |
| **Objective** | Boot2Root - Capture both flags |

---

## 🖥️ Machine Specifications

| Component | Detail |
|---|---|
| **Operating System** | Ubuntu 14.04.6 LTS (32-bit) |
| **Kernel** | Linux 4.4.0-142-generic i686 |
| **Hostname** | Chinmai |
| **VM Platform** | VMware Workstation Pro |
| **Network Mode** | NAT |
| **RAM** | 1 GB |
| **Disk** | 2 GB |

### Open Ports

| Port | Service | Purpose |
|---|---|---|
| **22/tcp** | OpenSSH | Remote access |
| **80/tcp** | Apache HTTPD | Web server with clues |

### Closed Ports (originally open)

| Port | Service | Action Taken |
|---|---|---|
| **139/tcp** | SMB (NetBIOS) | Disabled via firewall |
| **445/tcp** | SMB (CIFS) | Disabled via firewall |

---

## 👤 User Accounts

### Existing Users (Preserved from Original)
| Username | Role |
|---|---|
| `wavex` | Original user - credentials in original SMB flag |
| `aveng` | Original user - credentials in `/usr/share/av/westsidesecret/ififoregt.sh` |

### New Users Created
| Username | Password | How to Discover |
|---|---|---|
| `CTF` | Hidden on website | HTML comments + `/hidden/secret.html` |
| `CTF1` | Hidden on website | HTML comments + `/hidden/secret.html` |
| `CTF2` | Hidden on website | Base64 on `/tools.html` + `/hidden/secret.html` |

**Note**: Passwords follow the pattern `[Place][Symbol][Numbers]` with leet speak substitutions.

---

## 🏁 Flag Locations

| Flag | Path | Format |
|---|---|---|
| **User Flag** | `/home/a/Flag1.txt` | `CTF{...}` |
| **Root Flag** | `/root/ififoregt.sh` | `CTF{...}` |

---

## 🌐 Website Details

The web server hosts a professional cybersecurity profile page with **hidden clues**
embedded throughout the source code.

### Hidden Clue Locations

| Location | What's Hidden | Discovery Method |
|---|---|---|
| **HTML Comments** | Password pattern hints | View page source |
| **CSS (`style.css`)** | ROT13-encoded usernames | Check comments in CSS |
| **JavaScript (`hints.js`)** | Base64-encoded usernames + console hints | View JS source |
| **`/robots.txt`** | Hidden directory paths | Standard enumeration |
| **`/hidden/notes.txt`** | Credential distribution map | Directory discovery |
| **`/hidden/secret.html`** | Session logs with plaintext passwords | Directory discovery |
| **`/tools.html`** | Base64-encoded full credentials | Directory discovery |

### Password Pattern
All passwords follow a consistent pattern for deduction:
- `[Place/City/State]` + `[Symbol (#, @, $)]` + `[Numbers]`
- Uses leet speak (e.g., e→3, a→@, o→0, i→1, s→$)

---

## 🖼️ Steganography Challenge

| Item | Detail |
|---|---|
| **Image Location** | `/home/kali/Desktop/resume-1.png` |
| **Hidden File** | `resume.png` (Professional resume) |
| **Tool Used** | `steghide` |
| **Extraction Command** | `steghide extract -sf profile_image.png` |
| **Passphrase** | Hidden within the website clues |

---

## 🔧 Setup Instructions

### VMware Workstation Pro

1. Download the OVA/VM file from the link below
2. Open VMware Workstation Pro
3. Go to **File** → **Open** → Select the VM file
4. Set the network adapter to **NAT mode**
5. Power on the VM

### Finding the IP Address

```bash
# From your Kali/attack machine:
sudo netdiscover -r 192.168.x.0/24
# or
sudo nmap -sn 192.168.x.0/24
