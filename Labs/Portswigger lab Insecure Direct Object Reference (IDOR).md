# Vulnerability Report — Insecure Direct Object Reference (IDOR)

## 1. Vulnerability Overview
- **Name:** Insecure Direct Object Reference (IDOR)
- **Severity:** High
- **Location:** /files/
- **Tool Used:** Browser only

## 2. Description
The application stores chat transcripts as static files
on the server with sequential numeric names (/files/1.txt,
/files/2.txt). The server does not verify whether the
requesting user owns the file. Any authenticated user
can access any file by simply changing the number in
the URL, exposing other users' private conversations
and sensitive data such as passwords.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Open Live Chat and click View Transcript
3. Notice the URL: /files/2.txt
4. Change the number to: /files/1.txt
5. Read carlos chat log containing his password
6. Login as carlos using the discovered password

## 4. Evidence
 <img width="952" height="687" alt="Screenshot 2026-07-07 212155" src="https://github.com/user-attachments/assets/2b24a9fc-2682-4a2c-af93-515ace480705" />
<img width="1897" height="911" alt="Screenshot 2026-07-07 212255" src="https://github.com/user-attachments/assets/98275e83-2d14-4cc3-9b38-bb807a3b4d9f" />
<img width="1917" height="1020" alt="Screenshot 2026-07-07 212735" src="https://github.com/user-attachments/assets/994bb3e7-2362-4202-a8c1-9b609c19741d" />
<img width="1917" height="1016" alt="Screenshot 2026-07-07 212821" src="https://github.com/user-attachments/assets/ef1f140c-b65f-4974-93b7-4e356da19c5c" />


## 5. Impact
Any authenticated user can read private chat logs
of all other users. Sensitive data including passwords,
personal information, and private conversations are
fully exposed. Complete horizontal privilege escalation.

## 6. Remediation
- Verify server-side that the requesting user owns
  the file before returning it
- Use non-predictable random file names (UUID)
  instead of sequential numbers
- Implement proper authorization checks on every
  file access request
- Never trust user-supplied references without
  ownership verification
