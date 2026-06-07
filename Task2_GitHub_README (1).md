# 🔍 Task 2: Network Security & Scanning

> **Intern:** Diwakar Chandra | **ID:** APSPL2632803  
> **Timeline:** Days 13–24 | **Program:** ApexPlanet Cybersecurity Internship

---

## 🎯 Objective
Learn reconnaissance, scanning, and network traffic analysis.

---

## 📋 Topics Covered

### 1. Reconnaissance
| Type | Tools | Purpose |
|------|-------|---------|
| Passive | Whois, Nslookup, Shodan, Google Dorking | Gather info without alerting target |
| Active | Ping Sweep, Banner Grabbing | Directly probe the target |

**Google Dorking Examples:**
```
site:target.com filetype:pdf
intitle:"index of"
inurl:admin
inurl:login
```

---

### 2. Nmap Port Scanning

```bash
# Discover live hosts
nmap -sn 192.168.56.0/24

# TCP SYN Stealth Scan
nmap -sS 192.168.56.102

# UDP Scan
nmap -sU 192.168.56.102

# Service Version Detection
nmap -sV 192.168.56.102

# OS Detection
nmap -O 192.168.56.102

# Full Aggressive Scan
nmap -A 192.168.56.102

# Save results to file
nmap -A 192.168.56.102 -oN scan_results.txt
```

**Open Ports Found on Metasploitable2:**

| Port | Service | Version | Risk |
|------|---------|---------|------|
| 21 | FTP | vsftpd 2.3.4 | 🔴 Critical |
| 22 | SSH | OpenSSH 4.7p1 | 🟡 Medium |
| 23 | Telnet | Linux telnetd | 🟠 High |
| 80 | HTTP | Apache 2.2.8 | 🟠 High |
| 3306 | MySQL | 5.0.51a | 🟠 High |
| 8180 | HTTP-Alt | Apache Tomcat | 🟠 High |

---

### 3. Vulnerability Scanning (OpenVAS)

```bash
# Start OpenVAS
sudo gvm-start

# Access web interface
# https://127.0.0.1:9392

# Steps:
# 1. Create Target → IP: 192.168.56.102
# 2. Create Task → Full and Fast scan
# 3. Run scan → Wait ~45 min
# 4. View report → Export as PDF
```

**Critical Vulnerabilities Found:**
- 🔴 **vsftpd 2.3.4 Backdoor** (Port 21) — Remote Code Execution
- 🔴 **UnrealIRCd Backdoor** (Port 6667) — Remote Code Execution
- 🟠 **Samba Shell Injection** (Port 445) — Command Execution
- 🟠 **MySQL No Root Password** (Port 3306) — Full DB Access

---

### 4. Wireshark Packet Analysis

```
# Key Filters Used:
http                          → HTTP traffic
ftp                           → FTP traffic (credentials in plaintext!)
dns                           → DNS queries
tcp.flags.syn == 1            → SYN packets (for SYN flood analysis)
ip.addr == 192.168.56.102     → Filter by target IP
```

**FTP Credential Capture:**
```
USER: msfadmin    ← Visible in plaintext!
PASS: msfadmin    ← Visible in plaintext!
```
> ⚠️ This proves why FTP is insecure — always use SFTP instead!

**SYN Flood Simulation:**
```bash
# Simulate with hping3
hping3 -S --flood -V -p 80 192.168.56.102

# Wireshark shows massive SYN packets with no ACK response
# Mitigation: SYN cookies + rate limiting + firewall rules
```

---

### 5. Firewall with iptables

```bash
# View current rules
iptables -L -v -n

# Block all incoming by default
iptables -P INPUT DROP

# Allow established connections
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Block Telnet (insecure)
iptables -A INPUT -p tcp --dport 23 -j DROP

# Block FTP (insecure)
iptables -A INPUT -p tcp --dport 21 -j DROP

# SYN flood protection
iptables -A INPUT -p tcp --syn -m limit --limit 1/s -j ACCEPT
iptables -A INPUT -p tcp --syn -j DROP

# Save rules
iptables-save > /etc/iptables/rules.v4
```

---

## 🔑 Key Takeaways

1. **Reconnaissance is the first step** — know your target before attacking
2. **Nmap reveals everything** — open ports = potential entry points
3. **vsftpd 2.3.4 has a backdoor** — never use outdated software
4. **FTP is dangerous** — credentials visible in plain text on the network
5. **Firewalls reduce attack surface** — always disable unused services/ports
6. **Vulnerability scanners save time** — OpenVAS finds CVEs automatically

---

## 📁 Repository Structure

```
task2-network-security/
├── README.md
├── reports/
│   └── Task2_Network_Security_Report.pdf
├── scan_results/
│   ├── nmap_scan.txt
│   └── openvas_report.pdf
├── wireshark/
│   └── ftp_capture_notes.md
└── firewall/
    └── iptables_rules.sh
```

---

## 📌 Deliverables

| Deliverable | Status |
|-------------|--------|
| Nmap Scan Report | ✅ Completed |
| OpenVAS Vulnerability Report | ✅ Completed |
| Wireshark Packet Analysis | ✅ Completed |
| iptables Firewall Demo | ✅ Completed |
| GitHub Repository | ✅ Completed |
| 5-min Demo Video | ✅ Completed |

---

## 🔗 Submission Links
- **LinkedIn Video:** [Add your LinkedIn video link]
- **GitHub:** https://github.com/Diwakar0101/apexplanet-cybersecurity-internship

---

*ApexPlanet Cybersecurity Internship | www.apexplanet.in*
