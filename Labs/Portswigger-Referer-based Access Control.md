# Vulnerability Report — Referer-based Access Control

## 1. Vulnerability Overview
- **Name:** Referer-based Access Control
- **Severity:** Critical
- **Location:** /admin-roles
- **Tool Used:** Burp Suite Repeater

## 2. Description
The server grants access to admin functionality based
on the Referer header instead of verifying the user's
actual permissions. An attacker can forge the Referer
header to make the server believe the request originated
from the admin panel, bypassing all access controls.

## 3. Steps to Reproduce
1. Login as administrator and promote carlos
2. Capture the request in Burp Repeater:
   GET /admin-roles?username=carlos&action=upgrade
   Referer: https://LAB-URL/admin
3. Open incognito and login as wiener:peter
4. Copy wiener session cookie into the Repeater request
5. Change username=carlos to username=wiener
6. Keep the Referer header pointing to /admin
7. Send request — wiener promoted to Admin ✅

## 4. Evidence
 <img width="1919" height="1010" alt="Screenshot 2026-08-10 213755" src="https://github.com/user-attachments/assets/97c92961-c801-417d-8828-d70c785a34eb" />
<img width="1919" height="1016" alt="Screenshot 2026-08-10 213903" src="https://github.com/user-attachments/assets/2500c519-952f-4a50-a9d7-6f280e39d218" />
<img width="1919" height="1015" alt="Screenshot 2026-08-10 213925" src="https://github.com/user-attachments/assets/a7aefebc-1471-4445-9577-a08995444925" />

## 5. Impact
Any authenticated user can escalate their privileges
to Administrator by forging the Referer header.
The Referer header is fully controlled by the client
and cannot be trusted for authorization decisions.

## 6. Remediation
- Never use the Referer header for access control
- Enforce server-side authorization based on
  user session and role only
- Verify user permissions independently on
  every request regardless of request origin
