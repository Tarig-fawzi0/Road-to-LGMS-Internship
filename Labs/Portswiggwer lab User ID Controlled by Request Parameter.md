# Vulnerability Report — User ID Controlled by Request Parameter

## 1. Vulnerability Overview
- **Name:** Insecure Direct Object Reference (IDOR)
- **Severity:** High
- **Location:** /my-account?id=
- **Tool Used:** Browser only

## 2. Description
The application uses the username as a direct reference
in the URL parameter to retrieve account data. The server
does not verify that the logged-in user matches the
requested ID. Any authenticated user can access another
user's account data by changing the ID parameter in the URL.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Navigate to /my-account?id=wiener
3. Change the ID parameter to: /my-account?id=carlos
4. Server returns carlos account page with his API Key
5. Copy the API Key and submit as solution

## 4. Evidence
 <img width="950" height="796" alt="Screenshot 2026-07-07 175839" src="https://github.com/user-attachments/assets/27f0b864-6b6c-4a95-b893-32c4360562b3" />
<img width="952" height="812" alt="Screenshot 2026-07-07 175944" src="https://github.com/user-attachments/assets/23ff05f8-5e68-4cee-802d-370d9d88b872" />


## 5. Impact
Any authenticated user can access sensitive data
belonging to other users including API Keys, emails,
and personal information. Full horizontal privilege
escalation across all user accounts.

## 6. Remediation
- Verify server-side that the session user matches
  the requested account ID
- Never use predictable user-supplied values as
  direct object references
- Use indirect references mapped server-side
  instead of direct IDs in URLs
