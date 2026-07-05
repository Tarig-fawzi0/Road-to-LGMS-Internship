# Vulnerability Report — User Role Controlled by Request Parameter

## 1. Vulnerability Overview
- **Name:** User Role Controlled by Request Parameter
- **Severity:** Critical
- **Location:** /admin
- **Tool Used:** Burp Suite Interceptor

## 2. Description
The application determines the user's role based on
a cookie value (Admin=false/true) supplied by the client.
The server trusts this value without verifying it against
the database. An attacker can simply change Admin=false
to Admin=true in the cookie to gain full admin privileges.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Attempt to access /admin — access denied
3. Intercept the request in Burp Suite
4. Locate the cookie: Admin=false
5. Change the cookie to: Admin=true
6. Forward the request
7. Full admin access granted
8. Delete carlos account

## 4. Evidence
 <img width="1917" height="1013" alt="Screenshot 2026-07-05 195343" src="https://github.com/user-attachments/assets/9633a898-d7a6-4370-a865-e8c9abaea954" />
<img width="1917" height="1015" alt="Screenshot 2026-07-05 200134" src="https://github.com/user-attachments/assets/a508dfb7-2ef9-4a64-8125-73d85731ed53" />


## 5. Impact
Any authenticated user can escalate their privileges
to Admin level by modifying a single cookie value.
Full administrative takeover of the application.

## 6. Remediation
- Never trust client-supplied values for authorization
- Store user roles server-side in the database only
- Verify permissions on every request against
  the database, not the cookie
- Use signed and encrypted tokens if roles must
  be stored client-side
