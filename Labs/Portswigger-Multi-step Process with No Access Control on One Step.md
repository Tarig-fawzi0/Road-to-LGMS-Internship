# Vulnerability Report — Multi-step Process with No Access Control on One Step

## 1. Vulnerability Overview
- **Name:** Multi-step Process with Missing Access Control
- **Severity:** Critical
- **Location:** /admin-roles
- **Tool Used:** Burp Suite Repeater

## 2. Description
The application implements a multi-step process for
changing user roles. Access control is enforced on
the first step only. The confirmation step assumes
that anyone who reaches it has already passed the
first step's authorization check. An attacker can
skip directly to the confirmation step with a
non-admin session and successfully escalate privileges.

## 3. Steps to Reproduce
1. Login as administrator and promote carlos
2. Capture the confirmation request in Burp Repeater:
   action=upgrade&confirmed=true&username=carlos
3. Open incognito window and login as wiener:peter
4. Copy wiener session cookie into the Repeater request
5. Change username=carlos to username=wiener
6. Send request — receive 302 Found
7. wiener is now Administrator ✅

## 4. Evidence
 <img width="1919" height="1019" alt="Screenshot 2026-08-10 201452" src="https://github.com/user-attachments/assets/e5108ecc-72db-4e96-b1f1-f7fa35dd8bb8" />
<img width="1914" height="1016" alt="Screenshot 2026-08-10 201708" src="https://github.com/user-attachments/assets/cb0b4df0-94ff-49f2-af42-56aa58befcde" />
<img width="1903" height="989" alt="Screenshot 2026-08-10 201809" src="https://github.com/user-attachments/assets/ddcb1d1c-8422-4bde-aa11-735898522cd6" />
<img width="1911" height="1015" alt="Screenshot 2026-08-10 201925" src="https://github.com/user-attachments/assets/831c84b2-d8e7-4ddd-b8ec-4000b3d890aa" />

## 5. Impact
Any authenticated user can escalate their privileges
to Administrator by skipping directly to the
confirmation step of the role-change process.
Complete vertical privilege escalation and full
application takeover.

## 6. Remediation
- Enforce access control independently on every
  step of any multi-step process
- Never assume a user passed previous steps
- Validate session and permissions server-side
  on every single request regardless of step order
- Track completed steps server-side not client-side
