# Vulnerability Report — SQL Injection Login Bypass

## 1. Vulnerability Overview
- **Name:** SQL Injection Authentication Bypass
- **Severity:** Critical
- **Location:** /login
- **Tool Used:** Browser

## 2. Description
The login form passes user input directly into the
SQL query without sanitization. By injecting a
comment sequence into the username field, the
password check is completely bypassed, allowing
login as any user without knowing their password.

## 3. Steps to Reproduce
1. Navigate to /login
2. Enter username: administrator'--
3. Enter any password
4. Login successful as administrator

## 4. Evidence
 <img width="1914" height="1009" alt="Screenshot 2026-08-15 012003" src="https://github.com/user-attachments/assets/543f6720-33e5-45c5-b6e4-3754ba1d5b91" />
 
<img width="1919" height="1010" alt="Screenshot 2026-08-15 012204" src="https://github.com/user-attachments/assets/f21a3d3d-31d5-41fd-9d51-35697e3484a9" />
<img width="1919" height="1018" alt="Screenshot 2026-08-15 012222" src="https://github.com/user-attachments/assets/526cc32a-2317-4d2f-81ba-7daceba37034" />
<img width="1914" height="1016" alt="Screenshot 2026-08-15 012737" src="https://github.com/user-attachments/assets/29e26a1f-f57e-4b8e-8903-c11cd3a2a204" />

## 5. Impact
An attacker can login as any user including
administrators without knowing their password.
Complete authentication bypass and full
application takeover.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement proper input validation
- Use an ORM (Object Relational Mapper)
