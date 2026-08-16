# Vulnerability Report — SQL Injection UNION Attack, Determining Number of Columns

## 1. Vulnerability Overview
- **Name:** SQL Injection UNION Attack
- **Severity:** Critical
- **Location:** /filter?category=
- **Tool Used:** Browser / Burp Suite

## 2. Description
The application is vulnerable to SQL injection in the
category parameter. To perform a UNION attack and
retrieve data from other tables, the number of columns
in the original query must first be determined. This
is achieved using ORDER BY or NULL enumeration until
the correct number is found.

## 3. Steps to Reproduce
1. Inject ORDER BY to find column count:
   ' ORDER BY 1--  ✅
   ' ORDER BY 2--  ✅
   ' ORDER BY 3--  ✅
   ' ORDER BY 4--  ❌ → column count = 3
2. Confirm using NULL method:
   ' UNION SELECT NULL,NULL,NULL-- ✅

## 4. Evidence
 <img width="1590" height="811" alt="Screenshot 2026-08-17 014638" src="https://github.com/user-attachments/assets/a4fffefc-dcd3-41dd-ad86-97ac83e54fa8" />
<img width="1612" height="925" alt="Screenshot 2026-08-17 014736" src="https://github.com/user-attachments/assets/1c4de9b8-09e0-4a8a-9914-270a5916b045" />
<img width="1911" height="982" alt="Screenshot 2026-08-17 014837" src="https://github.com/user-attachments/assets/34d60547-553e-4cb7-94d7-5da07ffb8044" />


## 5. Impact
Knowing the column count allows an attacker to
perform UNION attacks to retrieve sensitive data
from any table in the database including usernames,
passwords, and other confidential information.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement input validation and WAF rules
- Use an ORM (Object Relational Mapper)
