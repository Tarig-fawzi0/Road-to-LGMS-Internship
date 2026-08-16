# Vulnerability Report — SQL Injection in WHERE Clause

## 1. Vulnerability Overview
- **Name:** SQL Injection in WHERE Clause
- **Severity:** Critical
- **Location:** /filter?category=
- **Tool Used:** Browser

## 2. Description
The application passes user input directly into the
SQL WHERE clause without sanitization. An attacker
can inject SQL code to modify the query logic and
retrieve hidden or unauthorized data.

## 3. Steps to Reproduce
1. Navigate to /filter?category=Gifts
2. Modify the category parameter:
   /filter?category=Gifts'+OR+1=1--
3. All products including hidden ones are returned

## 4. Evidence
 <img width="1914" height="1013" alt="Screenshot 2026-08-15 010448" src="https://github.com/user-attachments/assets/864dac7f-94d7-4c66-a847-0e3c09c99e07" />
<img width="1919" height="1010" alt="Screenshot 2026-08-15 010715" src="https://github.com/user-attachments/assets/ed63df97-cd31-494e-b9ab-267e96b93631" />


## 5. Impact
An attacker can retrieve all hidden data from the
database, bypass business logic, and potentially
access sensitive information from other tables.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement input validation and sanitization
- Use an ORM (Object Relational Mapper)
