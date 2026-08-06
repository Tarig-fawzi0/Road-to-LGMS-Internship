# Vulnerability Report — User Role Can Be Modified in User Profile

## 1. Vulnerability Overview
- **Name:** User Role Modification via User Profile
- **Severity:** Critical
- **Location:** /my-account
- **Tool Used:** Burp Suite Repeater

## 2. Description
The application allows users to modify their own role
by adding a roleid parameter to the profile update
request. The server accepts and processes this parameter
without verifying if the user has permission to change
their own role, allowing any user to escalate their
privileges to Administrator.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Navigate to /my-account
3. Update email and intercept the request in Burp Suite
4. Notice the JSON body:
   {"email":"test@test.com"}
5. Add roleid parameter to the request:
   {"email":"test@test.com","roleid":2}
6. Forward the request
7. Navigate to /admin — full access granted
8. Delete carlos

## 4. Evidence
 <img width="1919" height="1006" alt="Screenshot 2026-08-07 024935" src="https://github.com/user-attachments/assets/744396f7-9689-4e99-81f5-04190136ed33" />
<img width="1919" height="1005" alt="Screenshot 2026-08-07 024815" src="https://github.com/user-attachments/assets/8407d7c1-ee50-4f91-a6a0-dcabc886b35c" />



## 5. Impact
Any authenticated user can escalate their privileges
to Administrator level by adding a single parameter
to a normal profile update request. Complete vertical
privilege escalation and full application takeover.

## 6. Remediation
- Never accept role or privilege parameters
  from user-supplied input
- Enforce role assignment server-side only
- Strip any unauthorized parameters from
  user profile update requests
- Implement strict input validation and
  whitelist only expected parameters
