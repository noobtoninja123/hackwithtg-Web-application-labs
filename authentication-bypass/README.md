# Authentication Bypass – PortSwigger Lab

## 🎯 Objective
Bypass the login authentication mechanism by identifying subtle response differences.

---

## 🛠 Tools Used
- Burp Suite Community Edition
- Firefox
- PortSwigger Web Security Academy

---

## 🔎 Initial Observation

- All login attempts returned **HTTP 200 OK**
- However, response content length differed slightly

Example:

| Username Attempt | Status Code | Response Length |
|------------------|------------|-----------------|
| admin1           | 200        | 3677            |
| administrator    | 200        | 3788            |

The difference in response length indicated a valid username.

---

## ⚙️ Exploitation Steps

1. Intercept login request using Burp Suite.
2. Send request to Intruder.
3. Use username wordlist.
4. Observe response length differences.
5. Identify valid username.
6. Perform password brute-force on identified username.

---

## 🧠 Key Lesson Learned

- Status codes alone are not reliable.
- Always analyze response length and subtle variations.
- Authentication logic flaws can leak user enumeration information.

---

## 🛡 Prevention

- Implement uniform responses.
- Avoid revealing username validity.
- Use rate limiting and account lockout mechanisms.

