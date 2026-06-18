Password Brute-Force via Password ChangeExploit the password change functionality to brute-force another user's password and gain access to their account.

Vulnerability

The application allows unlimited password change attempts without proper rate limiting or account protection mechanisms.

Steps
1. Login with my account

Login using the credentials provided by the lab.

 Intercept the password change request

Capture the password change request using Burp Suite Proxy.

<img width="1918" height="1071" alt="Screenshot 2026-06-17 054326" src="https://github.com/user-attachments/assets/2f27c5dc-7a53-4989-ad46-32ed96d2de99" />


3. Send request to Intruder

Send the password change request to Burp Intruder and configure the payload position for the password field.

<img width="1907" height="1021" alt="Screenshot 2026-06-17 054300" src="https://github.com/user-attachments/assets/3d4977c3-d6b5-4cc1-94c4-0cf85aaa2c73" />


4. Start brute-force attack

Use the provided password list and launch the attack.



5. Identify the valid password

Observe the response length, status code, or response message to find the correct password.

<img width="1912" height="960" alt="Screenshot 2026-06-17 054633" src="https://github.com/user-attachments/assets/3b181140-1515-4737-9e39-25984c223e2a" />


6. Login as victim

Use the discovered password to login to the victim account.

<img width="1918" height="1031" alt="Screenshot 2026-06-17 054806" src="https://github.com/user-attachments/assets/69e064f6-9ca7-4d60-8f7d-14d32c6062a6" />


Impact

An attacker can brute-force user passwords through the password change functionality and gain unauthorized access to accounts.

Recommendation
Implement rate limiting.
Lock accounts after multiple failed attempts.
Require current password verification.
Monitor suspicious password change activity.
Key Learning
Password change functions must have brute-force protection.
Always test authentication features, not only the login page.
Burp Intruder can be used to identify valid credentials through response differences.
