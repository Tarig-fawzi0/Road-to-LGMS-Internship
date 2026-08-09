# Vulnerability Report — URL-based Access Control Bypass

## 1. Vulnerability Overview
- **Name:** URL-based Access Control Bypass
- **Severity:** Critical
- **Location:** /admin
- **Tool Used:** Burp Suite Repeater

## 2. Description
The front-end enforces access control based only on
the URL in the request line. The back-end framework
supports the X-Original-URL header which overrides
the actual URL. By sending a request to / while
setting X-Original-URL: /admin, the front-end
protection is bypassed entirely.

## 3. Steps to Reproduce
1. Attempt to access /admin — receive 403 Forbidden
2. Send request to Burp Repeater
3. Change URL to: GET /
4. Add header: X-Original-URL: /invalid
   → Returns "not found" confirming backend reads header
5. Change header to: X-Original-URL: /admin
   → Admin panel accessible
6. To delete carlos:
   GET /?username=carlos
   X-Original-URL: /admin/delete

## 4. Evidence
 <img width="1919" height="993" alt="Screenshot 2026-08-09 115908" src="https://github.com/user-attachments/assets/f0cd0cc7-ddcd-4f0b-ae71-a291d5b1a33c" />
<img width="1919" height="1023" alt="Screenshot 2026-08-09 120109" src="https://github.com/user-attachments/assets/bad62d8b-f188-4945-9ef1-49ae2c6a27ba" />
<img width="1919" height="1020" alt="Screenshot 2026-08-09 121115" src="https://github.com/user-attachments/assets/d38468ca-7d36-4249-8c3d-02178707da99" />


## 5. Impact
Any unauthenticated attacker can bypass front-end
access controls and access restricted admin functionality
by using the X-Original-URL header. Complete vertical
privilege escalation and full application compromise.

## 6. Remediation
- Enforce access control at the backend level
- Disable or ignore X-Original-URL header
- Never trust client-supplied headers for routing
- Implement consistent authorization checks
  regardless of how the request is routed
