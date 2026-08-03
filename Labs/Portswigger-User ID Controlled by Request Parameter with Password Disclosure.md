# Vulnerability Report — User ID Controlled by Request Parameter with Password Disclosure

## 1. Vulnerability Overview
- **Name:** Password Disclosure via Request Parameter
- **Severity:** Critical
- **Location:** /my-account?id=
- **Tool Used:** Browser / Burp Suite

## 2. Description
The application exposes the user's password in the
HTML response when accessing the account page. By
changing the ID parameter in the URL to another
user's username, an attacker can view that user's
password directly in the page source or response body.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Navigate to /my-account?id=wiener
3. Change the ID parameter to: /my-account?id=administrator
4. View the HTML response — administrator password
   is exposed in the password field
5. Login as administrator using the disclosed password
6. Access admin panel and delete carlos

## 4. Evidence
 <img width="1916" height="1002" alt="Screenshot 2026-08-03 112129" src="https://github.com/user-attachments/assets/f2893e22-5e98-473b-933c-e874ed75045d" />
<img width="1919" height="1010" alt="Screenshot 2026-08-03 112310" src="https://github.com/user-attachments/assets/81045575-6808-4bca-ade2-a6326fec9fea" />
<img width="1919" height="1010" alt="Screenshot 2026-08-03 112436" src="https://github.com/user-attachments/assets/684c408f-68ba-407d-b09a-892b6114fd19" />


## 5. Impact
An attacker can retrieve the password of any user
including administrators by simply changing the ID
parameter. This leads to full vertical and horizontal
privilege escalation and complete application takeover.

## 6. Remediation
- Never include passwords in HTML responses
- Enforce server-side authorization — verify the
  session user matches the requested account ID
- Use masked password fields that never return
  the actual password value from the server
- Implement proper access control on all
  account-related endpoints
