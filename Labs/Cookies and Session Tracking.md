# Cookies and Session Tracking

## Objective

Understand how web applications maintain user sessions using cookies.

---

## Practical Steps

1. Opened Burp Suite HTTP History.
2. Located a response containing Set-Cookie.
3. Identified the session cookie.
4. Observed subsequent requests carrying the cookie.
5. Analyzed how sessions are maintained.
 

<img width="1909" height="574" alt="image" src="https://github.com/user-attachments/assets/478edbb1-b363-4a21-9fb8-7a94a6d80e57" />

## Findings

Observed the server creating a session using the Set-Cookie header.

The browser stored the cookie and automatically included it in later requests.

---

## Lessons Learned

- Sessions allow web applications to recognize returning users.
- Servers create sessions using Set-Cookie headers.
- Browsers store cookies and resend them automatically.
- Session cookies are essential for authentication and user tracking.
