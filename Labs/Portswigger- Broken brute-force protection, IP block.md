# Vulnerability Report — Broken Brute-force Protection IP Block

## 1. Vulnerability Overview
- **Name:** Broken Brute-force Protection, IP Block
- **Severity:** High
- **Location:** /login
- **Tool Used:** Burp Suite Intruder + Custom Wordlist

## 2. Description
The application blocks an IP after 3 consecutive failed
login attempts. However, the failed attempt counter resets
to zero upon any successful login. By interleaving valid
credentials with brute-force attempts, an attacker can
bypass the IP block entirely and test unlimited passwords.

## 3. Steps to Reproduce
1. Prepare two wordlists in Pitchfork pattern:
   - usernames: wiener, carlos, carlos (repeating)
   - passwords: peter, guess1, guess2 (repeating)
2. Intercept login request in Burp Suite
3. Send to Intruder → Pitchfork attack type
4. Load both wordlists and start attack
5. Identify response with different length = correct password
6. Login as carlos with discovered password

## 4. Evidence
 <img width="1917" height="1026" alt="Screenshot 2026-07-03 124206" src="https://github.com/user-attachments/assets/ebaab58d-69c9-4392-a5e5-8362e2a1f85e" />
<img width="1917" height="1028" alt="Screenshot 2026-07-03 124221" src="https://github.com/user-attachments/assets/3699e8f6-06eb-4582-93d7-21e258d37729" />
<img width="1917" height="1025" alt="Screenshot 2026-07-03 124329" src="https://github.com/user-attachments/assets/84e45243-4b41-4222-b167-16c4facd85b4" />

 

## 5. Impact
Attacker can brute-force any account password without
triggering IP-based lockout, bypassing the only
brute-force protection mechanism in place.

## 6. Remediation
- Reset the counter only after a significant time period,
  not after a single successful login
- Implement account lockout independent of IP
- Use CAPTCHA after failed attempts
- Monitor and alert on abnormal login patterns
