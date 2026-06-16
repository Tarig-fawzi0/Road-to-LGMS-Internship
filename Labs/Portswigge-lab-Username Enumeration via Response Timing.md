Username Enumeration via Response Timing
Objective
Identify a valid username by analyzing response timing differences.
Vulnerability
The application leaks information through response times. Valid usernames take longer to process than invalid usernames.
What I Did
1.	Captured the login request using Burp Suite.
2.	Added the X-Forwarded-For header.
3.	Changed the header value to bypass IP-based protection.
4.	Sent requests with a long password.
5.	Compared response times.
6.	Found the valid username.
7.	Performed password testing and solved the lab.
Evidence
 <img width="1918" height="900" alt="Screenshot 2026-06-17 043553" src="https://github.com/user-attachments/assets/d1cabe5a-6143-4046-95f6-79e417002cfc" />
 <img width="1918" height="1023" alt="Screenshot 2026-06-17 043607" src="https://github.com/user-attachments/assets/f290f478-2299-4a1f-9157-308caac20e8f" />
<img width="1918" height="1012" alt="Screenshot 2026-06-17 043434" src="https://github.com/user-attachments/assets/196c1533-304a-4090-a2e9-ae9e50430100" />

Impact
An attacker can discover valid usernames and make brute-force attacks easier.
Fix
•	Use constant response times.
•	Use generic error messages.
•	Do not trust X-Forwarded-For headers from users.
What I Learned
I learned how response timing can reveal valid usernames and how X-Forwarded-For can be abused to bypass IP-based protections.

