# Vulnerability Report — Method-based Access Control Bypass

## 1. Vulnerability Overview
- **Name:** Method-based Access Control Bypass
- **Severity:** Critical
- **Location:** /admin-roles
- **Tool Used:** Burp Suite Repeater

## 2. Description
The application enforces access control on the POST
method only. The backend does not enforce the same
restrictions on GET requests to the same endpoint.
A non-admin user can bypass the access control by
changing the HTTP method from POST to GET, allowing
them to perform admin actions such as promoting their
own account to Administrator.

## 3. Steps to Reproduce
1. Login as administrator and promote carlos
2. Capture POST /admin-roles request in Burp Repeater
3. Open incognito window and login as wiener:peter
4. Copy wiener session cookie into the Repeater request
5. Send request — receive "Unauthorized"
6. Change method to POSTX — receive "missing parameter"
   confirming method-based protection exists
7. Change method to GET:
   GET /admin-roles?username=wiener&action=upgrade
8. Send request — receive 200 OK
9. wiener is now Administrator ✅

## 4. Evidence
 <img width="1919" height="1019" alt="Screenshot 2026-08-10 194750" src="https://github.com/user-attachments/assets/da693d28-d1a3-47dc-a9c8-5d0e4ae1c729" />


## 5. Impact
Any authenticated user can escalate their privileges
to Administrator by switching the HTTP method from
POST to GET on the admin endpoint. Complete vertical
privilege escalation and full application takeover.

## 6. Remediation
- Enforce access control on all HTTP methods
  not just POST
- Implement method-independent authorization checks
- Reject unexpected HTTP methods (POSTX, etc.)
- Apply consistent server-side authorization
  regardless of the request method used
