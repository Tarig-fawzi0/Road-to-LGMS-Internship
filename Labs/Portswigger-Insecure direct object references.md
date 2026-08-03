# Vulnerability Report — Insecure Direct Object References (IDOR)

## 1. Vulnerability Overview
- **Name:** Insecure Direct Object Reference (IDOR)
- **Severity:** High
- **Location:** /files/
- **Tool Used:** Browser only

## 2. Description
The application stores chat transcripts as static files
with sequential numeric names. The server exposes these
files through predictable URLs and does not verify that
the requester owns the requested transcript. Any
authenticated user can access any transcript by
changing the file number in the URL.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Open Live Chat and click View Transcript
3. Notice the file URL: /files/2.txt
4. Change the number to: /files/1.txt
5. Read carlos private chat log
6. Find carlos password in the transcript
7. Login as carlos using the discovered password

## 4. Evidence
 <img width="1918" height="1012" alt="Screenshot 2026-08-03 120052" src="https://github.com/user-attachments/assets/7840c629-1c05-41fb-b6fd-72b296fd93df" />
<img width="1918" height="1016" alt="Screenshot 2026-08-03 120246" src="https://github.com/user-attachments/assets/38e25cb5-f9b8-4412-b017-47dc0a8665c8" />
<img width="1916" height="1018" alt="Screenshot 2026-08-03 120343" src="https://github.com/user-attachments/assets/56ea5828-5bf0-495a-ac2b-a78eb9611530" />

## 5. Impact
Any authenticated user can read private chat logs
of all other users. Sensitive data including passwords
and private conversations are fully exposed. Complete
horizontal privilege escalation across all accounts.

## 6. Remediation
- Verify server-side that the requesting user owns
  the file before returning it
- Use non-predictable random file names (UUID)
  instead of sequential numbers
- Never expose direct file paths to the client
- Implement proper authorization checks on every
  file access request
