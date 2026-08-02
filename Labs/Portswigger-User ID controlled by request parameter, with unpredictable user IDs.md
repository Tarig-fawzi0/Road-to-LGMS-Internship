IDOR Lab: Unpredictable User IDs

Bug: Account page uses a GUID in the URL (/my-account?id=...) instead of a simple number. Looks safe since GUIDs can't be guessed — but the server never checks if the GUID belongs to you.

Fix (exploit) steps:

Log in as wiener:peter.
Browse the site (blog comments) and check page source — the victim carlos's GUID is leaked there (hidden in HTML, not guessed).
Copy that GUID.
Visit /my-account?id=<carlos-guid>.
You're now viewing carlos's account (API key etc.) → lab solved.

Lesson: Random/unguessable IDs ≠ security. You still need a real authorization check on the server, because IDs can leak elsewhere.
