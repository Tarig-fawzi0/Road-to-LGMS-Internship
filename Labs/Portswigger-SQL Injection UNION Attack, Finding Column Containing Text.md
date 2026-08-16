# Vulnerability Report — SQL Injection UNION Attack, Finding Column Containing Text

## 1. Vulnerability Overview
- **Name:** SQL Injection UNION Attack
- **Severity:** Critical
- **Location:** /filter?category=
- **Tool Used:** Burp Suite Repeater

## 2. Description
SQL Injection is a vulnerability that allows an attacker
to manipulate SQL queries through user input and access
data they are not authorized to see. In this case, after
determining the number of columns, we identify which
column accepts string data by injecting text values
one column at a time until the value appears in the
response.

## 3. Steps to Reproduce
2. Find text-compatible column:
   ' UNION SELECT 'test',NULL,NULL-- ❌
   ' UNION SELECT NULL,'test',NULL-- ✅
3. Inject the provided value in column 2:
   ' UNION SELECT NULL,'yDaJKC',NULL--
4. Value appears in the response ✅

## 4. Evidence
 <img width="1919" height="1024" alt="Screenshot 2026-08-17 040112" src="https://github.com/user-attachments/assets/86ef1d35-6efb-4f73-a1cf-f9166e22b7ed" />
<img width="1917" height="1017" alt="Screenshot 2026-08-17 040314" src="https://github.com/user-attachments/assets/49ff7c51-c35d-4ffa-b269-9ac015ed1ec2" />


## 5. Impact
Identifying the text-compatible column allows an
attacker to extract sensitive string data such as
usernames, passwords, and emails from any table
in the database using UNION attacks.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement input validation and WAF rules
- Use an ORM (Object Relational Mapper)
