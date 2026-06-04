# Lab: Username Enumeration via Subtly Different Responses

## Objective

Learn how to identify a valid username by analyzing subtle differences in login responses and then discover the correct password.

---

## Tools Used

* Burp Suite Community Edition
* Web Browser

---

## Steps

### 1. Open the Lab

Opened the PortSwigger lab and reviewed the objective.

 
---

### 2. Capture the Login Request

Captured the POST /login request using Burp Suite and sent it to Intruder.

 <img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/75da2c95-4a36-4887-ac13-a5a80f71e588" />


![Captured Request](./screenshots/02-captured-request.png)

---

### 3. Enumerate Usernames

Configured Intruder with a username wordlist and launched a Sniper attack.

By comparing response lengths, a valid username was identified.

Valid Username:

```text
carlos
```

<img width="940" height="493" alt="image" src="https://github.com/user-attachments/assets/6cbd093b-069b-4789-bb2c-51ef6f9e592a" />
 

 

### 4. Enumerate Passwords

Fixed the username as:

```text
carlos
```

and performed a password attack using a password wordlist.

 <img width="940" height="493" alt="image" src="https://github.com/user-attachments/assets/29303e15-1ffe-4110-89fd-d6caed345889" />


 

---

### 5. Identify Successful Login

One response returned:

```text
302 Found
```

which indicated successful authentication.

Valid Password:

```text
starwars
```
<img width="940" height="502" alt="image" src="https://github.com/user-attachments/assets/bb9e23c4-07bc-4085-9feb-3c44d2e878e7" />

 

 
---

### 6. Lab Solved

Logged in successfully using the discovered credentials and accessed the account page.

 

## Impact

An attacker can discover valid usernames and perform targeted password attacks, increasing the chance of account compromise.

---

## Remediation

* Use generic login error messages.
* Ensure all failed login responses have the same length.
* Implement rate limiting.
* Enable Multi-Factor Authentication (MFA).
* Monitor authentication attempts.

---

## What I Learned

* How username enumeration works.
* How to analyze response lengths.
* How to use Burp Intruder for authentication testing.
* How to identify successful login attempts.
* How to document security findings.
