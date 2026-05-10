# 🛡️ ApexPlanet Cybersecurity Internship — Task 1: Foundation & Environment Setup

> **Program:** Cybersecurity & Ethical Hacking Internship (60 Days)  
> **Organization:** ApexPlanet Software Pvt. Ltd.  
> **Timeline:** Days 1–12  
> **Intern:** Diwakar Chandra  
> **Offer Letter ID:** APSPL2632803

---

## 📋 Overview

This repository documents the completion of **Task 1** of the ApexPlanet Cybersecurity & Ethical Hacking Internship. The goal was to build strong fundamentals in cybersecurity, networking, and cryptography, and to set up a professional ethical hacking lab environment.

---

## 🎯 Objectives Completed

- [x] Understood the CIA Triad (Confidentiality, Integrity, Availability)
- [x] Explored 6 common threat types and 3 attack vectors
- [x] Set up a fully isolated virtual lab (Kali Linux + Metasploitable2 + DVWA)
- [x] Practiced 20+ essential Linux commands
- [x] Studied the OSI Model, TCP/IP, DNS, HTTP/HTTPS
- [x] Learned symmetric & asymmetric cryptography + hashing
- [x] Hands-on with OpenSSL (encrypt/decrypt messages)
- [x] Familiarized with Wireshark, Nmap, Burp Suite, Netcat

---

## 🔬 Lab Environment

| Component | Details |
|-----------|---------|
| Hypervisor | VirtualBox (Host-Only Network) |
| Attacker Machine | Kali Linux 2024.x — IP: 192.168.56.101 |
| Target Machine | Metasploitable2 — IP: 192.168.56.102 |
| Vulnerable Web App | DVWA (Damn Vulnerable Web App) |
| Network | 192.168.56.0/24 (isolated, no internet) |

---

## 📚 Concepts Covered

### 1. Cybersecurity Basics
- **CIA Triad** — Confidentiality, Integrity, Availability
- **Threat Types** — Phishing, Malware, DDoS, SQL Injection, Brute Force, Ransomware
- **Attack Vectors** — Social Engineering, Wireless Attacks, Insider Threats

### 2. Linux Fundamentals
```bash
# File System Navigation
cd /path/to/dir     # Change directory
ls -la              # List all files with permissions
pwd                 # Print working directory
find / -name file   # Search recursively

# Permissions
chmod 755 file      # Set permissions
chown user:group file  # Change ownership

# Package Management
apt update && apt upgrade   # Update system
apt install <package>       # Install package

# Networking
ifconfig / ip a     # View IP addresses
ping <target>       # Test connectivity
netstat -tulnp      # View open ports
traceroute <host>   # Trace route to host
```

### 3. OSI Model (Security Perspective)

| Layer | Name | Key Attack |
|-------|------|-----------|
| 7 | Application | SQL Injection, XSS, Phishing |
| 6 | Presentation | SSL stripping |
| 5 | Session | Session hijacking |
| 4 | Transport | SYN flood (DDoS) |
| 3 | Network | IP spoofing |
| 2 | Data Link | ARP poisoning |
| 1 | Physical | Hardware tampering |

### 4. Cryptography

| Type | Algorithm | Key Feature |
|------|-----------|------------|
| Symmetric | AES-256, DES | Same key for encrypt/decrypt |
| Asymmetric | RSA-2048, ECC | Public/private key pair |
| Hashing | SHA-256, MD5 | One-way, fixed-length output |
| Password Hashing | bcrypt, Argon2 | With salt + work factor |

### 5. OpenSSL Hands-On
```bash
# Generate RSA private key
openssl genrsa -out private.key 2048

# Extract public key
openssl rsa -in private.key -pubout -out public.key

# Encrypt a file with AES-256-CBC
openssl enc -aes-256-cbc -in message.txt -out message.enc -k secretpassword

# Decrypt the file
openssl enc -d -aes-256-cbc -in message.enc -out decrypted.txt -k secretpassword

# Generate SHA-256 hash
openssl dgst -sha256 message.txt

# Generate MD5 hash
openssl dgst -md5 message.txt
```

---

## 🛠️ Tools Used

### Wireshark
```
Purpose: Packet capture and network traffic analysis
Key Filters:
  http          → Capture HTTP traffic
  ftp           → Capture FTP (plaintext credentials visible!)
  dns           → Capture DNS queries
  tcp.flags.syn == 1  → Capture SYN packets only
  ip.addr == 192.168.56.102  → Filter by target IP

Finding: FTP credentials transmitted in PLAINTEXT → always use SFTP/FTPS
```

### Nmap
```bash
# Ping scan — discover live hosts
nmap -sn 192.168.56.0/24

# TCP SYN stealth scan
nmap -sS 192.168.56.102

# UDP scan
nmap -sU 192.168.56.102

# Service version detection
nmap -sV 192.168.56.102

# OS detection
nmap -O 192.168.56.102

# Full aggressive scan
nmap -A 192.168.56.102
```

**Metasploitable2 Open Ports Found:**
- 21/tcp — vsftpd 2.3.4 (vulnerable!)
- 22/tcp — OpenSSH 4.7p1
- 23/tcp — Telnet
- 80/tcp — Apache 2.2.8
- 3306/tcp — MySQL 5.0.51a

### Burp Suite
```
Mode: Intercepting Proxy
Config: Browser → 127.0.0.1:8080 → Burp → Target
Used: Intercepted HTTP requests to DVWA
      Modified parameters in Repeater
      Explored target scope configuration
```

### Netcat
```bash
# Set up a listener
nc -lvnp 4444

# Connect to listener
nc 192.168.56.101 4444

# Banner grabbing
nc 192.168.56.102 22    # Grabs SSH banner

# File transfer
# Sender: cat file.txt | nc -lvnp 4444
# Receiver: nc 192.168.56.101 4444 > received.txt
```

---

## 📁 Repository Structure

```
task1-foundation/
├── README.md               ← This file
├── report/
│   └── Task1_Lab_Setup_Report.docx
├── cheatsheets/
│   └── linux_cheatsheet.md
├── openssl_demo/
│   ├── encrypt_demo.sh
│   └── demo_output.txt
├── screenshots/
│   ├── kali_setup.png
│   ├── metasploitable_running.png
│   ├── nmap_scan_results.png
│   └── wireshark_capture.png
└── notes/
    ├── cia_triad_notes.md
    ├── networking_notes.md
    └── cryptography_notes.md
```

---

## 📝 Linux Cheat Sheet

```bash
# ─── NAVIGATION ───────────────────────────────────────
pwd                     # Current directory
ls -la                  # List all files with permissions
cd ~                    # Go to home directory
cd ..                   # Go up one level
find / -name "*.txt"    # Search for .txt files

# ─── PERMISSIONS ──────────────────────────────────────
chmod 777 file          # rwx for all
chmod 644 file          # rw-r--r-- (files)
chmod 755 dir           # rwxr-xr-x (dirs)
chown user:group file   # Change ownership
sudo su                 # Switch to root

# ─── PROCESS MANAGEMENT ───────────────────────────────
ps aux                  # List all processes
kill -9 PID             # Force kill process
top / htop              # Real-time process monitor
bg / fg                 # Background / foreground jobs

# ─── NETWORKING ───────────────────────────────────────
ifconfig                # Network interfaces (legacy)
ip a                    # Network interfaces (modern)
ip route                # Routing table
ping -c 4 target        # 4 ICMP pings
netstat -tulnp          # Listening ports
ss -tulnp               # Modern netstat
nslookup domain.com     # DNS lookup
whois domain.com        # Domain info

# ─── FILE OPERATIONS ──────────────────────────────────
cp source dest          # Copy file
mv source dest          # Move/rename
rm -rf dir              # Force delete directory
tar -czf out.tar.gz dir # Create compressed archive
tar -xzf file.tar.gz    # Extract archive
grep -r "text" /path    # Search text in files
cat file                # View file
less file               # Paginated view

# ─── PACKAGE MANAGEMENT ───────────────────────────────
apt update              # Refresh package list
apt upgrade             # Upgrade installed packages
apt install pkg         # Install package
apt remove pkg          # Remove package
dpkg -i file.deb        # Install .deb package
dpkg -l                 # List installed packages
```

---

## 🔑 Key Takeaways

1. **Never practice on real systems** — always use an isolated lab
2. **CIA Triad** is the foundation of every security decision
3. **Encryption in transit matters** — FTP sends passwords in plaintext, always use SFTP
4. **Nmap is powerful** — version detection reveals exploitable services
5. **Linux CLI is essential** — all security tools are terminal-based
6. **Cryptography underpins security** — understanding it helps both attack and defense

---

## 📌 Deliverables

| Deliverable | Status |
|-------------|--------|
| Lab Setup Report (DOCX) | ✅ Completed |
| GitHub Repo with Notes | ✅ Completed (this repo) |
| Linux Cheat Sheet | ✅ Completed |
| 5-min Video Walkthrough | ✅ Completed |
| Wireshark Packet Capture | ✅ Completed |
| OpenSSL Demo Script | ✅ Completed |

---

## 🔗 Submission Links

- **LinkedIn Video:** [Add your LinkedIn video link here]
- **GitHub Repo:** [This repository URL]
- **Offer Letter ID:** APSPL2632803

---

*This repository is part of the ApexPlanet Cybersecurity & Ethical Hacking Internship Program. All activities were performed in an isolated virtual lab for educational purposes only.*

**Website:** www.apexplanet.in | **Email:** info@apexplanet.in
