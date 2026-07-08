# Vulnerability Report — URL-based Access Control Bypass

## 1. Vulnerability Overview
- **Name:** URL-based Access Control Bypass
- **Severity:** Critical
- **Location:** /admin
- **Tool Used:** Burp Suite Repeater

## 2. Description
 The application enforces access control on the visible
URL only. By adding the X-Original-URL header, an
attacker can override the actual URL and access
restricted pages like /admin, bypassing all front-end
protection entirely.
## 3. Steps to Reproduce
1. Attempt to access /admin — receive 403 Forbidden
2. Intercept any request in Burp Suite
3. Send to Repeater
4. Change URL to: GET /
5. Add header: X-Original-URL: /admin
6. Send request — admin panel returned
7. To delete carlos add:
   X-Original-URL: /admin/delete?username=carlos

## 4. Evidence
<img width="1917" height="1016" alt="Screenshot 2026-07-08 170715" src="https://github.com/user-attachments/assets/28647f4f-8b87-4667-8933-06f6d6f88347" />
<img width="1917" height="1021" alt="Screenshot 2026-07-08 170917" src="https://github.com/user-attachments/assets/de5f51fa-7f8a-495e-99c9-bfbb23b6fb2a" />
 <img width="1916" height="1016" alt="Screenshot 2026-07-08 171333" src="https://github.com/user-attachments/assets/f1091416-dcaa-469f-8ebb-09f11cce370f" />


## 5. Impact
Any unauthenticated attacker can bypass URL-based
access controls and access restricted functionality
including the admin panel. Complete vertical privilege
escalation and full application compromise.

## 6. Remediation
- Enforce access control at the backend level
  not just the URL level
- Disable or ignore X-Original-URL header
- Never trust client-supplied headers for
  routing or access control decisions
- Implement consistent authorization checks
  regardless of how the request is routed
