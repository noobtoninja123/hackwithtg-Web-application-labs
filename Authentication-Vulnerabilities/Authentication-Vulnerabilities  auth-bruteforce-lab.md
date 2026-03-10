Authentication Brute Force Lab

## Lab Overview
This lab demontrates how attackers exploit weak authentication protections to perform brute-force attacks.

##Target
Damn Vulnerable Web Application (DVWA).

##Tools
BurpSuite
Intruder
Browser

## Methodology
Step 1 - i login with invalid credentials. the login request was captured using burp suite, by then my proxy is already runnin![WhatsApp Image 2026-03-10 at 8 46 09 AM](https://github.com/user-attachments/assets/45d2bd85-4d56-4e48-b1dc-70c049aa2e4d)
.
Step 2 - i sent the request to intruder and highlighted the password value and added a payload makers to it.
Step 3 - i set the payload type and include a password list.
Step 4 - i starts the attack.
Step 5 - After the attack was finished i checked for the responses and results and i looked for the one with different length.
Step 6 - i successfully bruteforce the password and logged in as admin user.![WhatsApp Image 2026-03-10 at 8 46 08 AM](https://github.com/user-attachments/assets/bb740af2-0714-43ed-b79a-5b073d7dde0b)
## why it worked
- No Rate Limiting

- No Account Lockout
- No Login Delay
- Weak Password Policy.

## How Developers Should Fix This
- Rate Limiting E.g max 5 login attempts per minute.
- Account lockout e.g lock account after failed attempts.
- Captcha: stops automated attacks.
- Multi-factor Authentication; even if password is guessed, attacker still ned second factor to access the account.

Akabuogu ThankGod
Web App Pentester| Cybersecurity Content Creator| A Cybersecurity practitioner building in public.
