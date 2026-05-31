# PortSwigger Lab - 2FA Simple Bypass

## Lab Information

- Category: Authentication
- Difficulty: Apprentice
- Lab: 2FA Simple Bypass
- Status: Solved

---

## Objective

Access Carlos's account without completing the 2FA verification step.

---

## Credentials Provided

### Attacker Account

Username: wiener

Password: peter

### Victim Account

Username: carlos

Password: montoya

---

## Vulnerability Type

Broken Authentication

2FA Bypass

---

## Understanding The Application Flow

Normal authentication process:

Username + Password
↓
Login Success
↓
2FA Verification
↓
My Account

Expected behavior:

The application should verify that the user successfully completed the second authentication factor before granting access to protected resources.

---

## Testing Process

### Step 1

Login using:

wiener : peter

---

### Step 2

Observe the redirection:

/login
↓
/login2

The application requests a 2FA verification code.

---

### Step 3

Without entering the verification code, manually browse to:

/my-account

---

### Result

The account page becomes accessible.

This confirms that the application does not verify completion of the second authentication factor before granting access.

---

### Step 4

Logout.

---

### Step 5

Login using victim credentials:

carlos : montoya

---

### Step 6

Again the application redirects to:

/login2

---

### Step 7

Without entering the 2FA code, manually change the URL to:

/my-account

---

### Result

Successfully accessed Carlos's account.

Lab solved.

---

## Root Cause

The application validates the username and password but fails to enforce the second authentication factor on protected endpoints.

The server trusts the user session before the 2FA process is completed.

---

## Security Impact

An attacker with valid credentials can:

- Bypass 2FA
- Access victim accounts
- Read sensitive information
- Perform actions as the victim

---

## Evidence

### Screenshot 1

Login redirected to /login2.

 <img width="1919" height="692" alt="image" src="https://github.com/user-attachments/assets/fa8bcd79-81e7-491b-9904-91d93c7c0873" />


---

### Screenshot 2

Accessing /my-account without entering 2FA.

 <img width="1912" height="1025" alt="image" src="https://github.com/user-attachments/assets/c6ac7fb3-2a71-40db-a65d-e6d34ccfd7e2" />


---

### Screenshot 3

Carlos account successfully accessed.

![Uploading image.png…]()


---

## Key Burp Suite Skills Practiced

- Proxy
- HTTP History
- Request Analysis
- Response Analysis
- Authentication Flow Analysis
- Session Management Observation

---

## Lessons Learned

- 2FA must always be enforced server-side.
- Protected endpoints must verify authentication state.
- URL redirection alone is not security.
- Authentication workflows should be tested for logic flaws.
