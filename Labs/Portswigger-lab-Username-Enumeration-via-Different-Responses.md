Objective

The objective of this lab is to identify a valid username by analyzing differences in authentication responses and then discover the correct password using Burp Suite Intruder.

Vulnerability Overview

Username Enumeration occurs when an application reveals whether a username exists through different error messages, response lengths, status codes, or response times.

This information can help attackers identify valid accounts and significantly improve the success rate of brute-force attacks.

Tools Used
Burp Suite Community Edition
Web Browser
PortSwigger Web Security Academy
Testing Methodology
Step 1 - Capture Login Request

Intercept a login request using Burp Suite Proxy.

 <img width="1824" height="839" alt="image" src="https://github.com/user-attachments/assets/7d47e029-831d-4d16-a1f4-c6ae56b809a2" />





Step 2 - Username Enumeration

Send the login request to Burp Intruder.

Configure:

Attack Type: Sniper
Payload Position: Username
Password: Static value

Example:

POST /login

username=§invalid-user§
password=test123

Run the attack using the provided username wordlist.

Screenshot

<img width="1919" height="810" alt="image" src="https://github.com/user-attachments/assets/4a9fb54f-ad4a-4b80-895c-6f999416209f" />



Step 3 - Analyze Responses

Compare:

Response Length
Error Messages
Status Codes

Observation:

Most responses returned: "Invalid username"
One response returned: "Incorrect password"

This revealed a valid username.

Screenshot

<img width="1912" height="990" alt="image" src="https://github.com/user-attachments/assets/d16f3d71-3b00-4a24-981c-3a334369cd43" />



Step 4 - Password Discovery

Fix the identified username and place the payload position on the password field.

Example:

POST /login

username=[VALID_USERNAME]
password=§password§

Run the attack using the password wordlist.

 <img width="1919" height="1068" alt="image" src="https://github.com/user-attachments/assets/9804cb0a-e4a9-480f-b3e9-dbe0f834678a" />




Step 5 - Successful Authentication

One request returned:

302 Found

This indicated a successful login.

The valid credentials were identified.

  <img width="993" height="839" alt="image" src="https://github.com/user-attachments/assets/fd15a288-5f8d-4772-ba5a-703196b2aa2b" />




Impact

An attacker can:

Enumerate valid usernames
Reduce brute-force complexity
Increase the success rate of credential attacks
Facilitate account compromise

Risk Level

Medium

Remediation
Use generic authentication error messages.
Return identical responses for failed logins.
Implement rate limiting.
Implement account lockout mechanisms.
Enable Multi-Factor Authentication (MFA).
Monitor authentication anomalies.

Example:

Invalid username or password


Lessons Learned
Authentication responses can leak sensitive information.
Response analysis is an important part of penetration testing.
Burp Suite Intruder can efficiently identify valid usernames.
Username Enumeration is often the first step before password attacks.


Skills Practiced
Authentication Testing
Username Enumeration
Burp Suite Intruder
Response Analysis
Password Brute Force Detection
Security Documentation

 
