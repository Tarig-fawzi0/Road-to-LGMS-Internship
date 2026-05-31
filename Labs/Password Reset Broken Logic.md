# Lab 03 - Password Reset Broken Logic

## Category
Authentication Vulnerabilities

## Platform
PortSwigger Web Security Academy

## Difficulty
Apprentice

---

## Objective

Reset another user's password by abusing a flaw in the password reset workflow.

---

## Scenario

The application provides a password reset feature.

A reset token is generated and sent to the user's email.

The vulnerability exists because the application trusts a user-controlled parameter during the password reset process.

---

## Credentials

Attacker:

Username: wiener

Password: peter

Victim:

Username: carlos

---

## Steps

### Step 1 - Request Password Reset

Navigate to:

Forgot Password

Submit:

wiener

---

### Step 2 - Obtain Reset Token

Open Email Client.

A reset email is received containing a temporary password reset token.

Example:

temp-forgot-password-token=xxxxxxxx

---

### Step 3 - Intercept Request

Enable Burp Suite Intercept.

Submit a new password.

Intercepted request:

POST /forgot-password

---

### Step 4 - Identify Vulnerable Parameter

The request contains:

username=wiener

---

### Step 5 - Modify Username

Change:

username=wiener

To:

username=carlos

---

### Step 6 - Forward Request

Forward the modified request.

The password of Carlos is reset using Wiener's token.

---

### Step 7 - Login as Carlos

Login using:

Username: carlos

Password: Password123!21

Successfully accessed Carlos's account.

---

## Root Cause

The password reset token was not bound to a specific account.

The application trusted the username parameter supplied by the client.

---

## Impact

- Account Takeover
- Unauthorized Password Reset
- Authentication Bypass

---

## Lessons Learned

Never trust user-controlled identifiers during password reset workflows.

Password reset tokens must be validated server-side and linked to a specific account.

---

## Screenshots

### Intercepted Password Reset Request
<img width="1421" height="608" alt="image" src="https://github.com/user-attachments/assets/b4325d89-ee0b-4929-948d-3b912dab1f66" />

 
### Modified Username Parameter

 <img width="1321" height="837" alt="image" src="https://github.com/user-attachments/assets/2ed4120a-12d1-436c-b5b3-bb7fe2f37298" />


### Successful Login as Carlos
<img width="1868" height="939" alt="image" src="https://github.com/user-attachments/assets/1ecfe2f7-342f-443f-a35f-3e9d44af42bb" />
