# Vulnerability Report — User ID Controlled by Request Parameter with Data Leakage in Redirect

## 1. Vulnerability Overview
- **Name:** Sensitive Data Leakage in Redirect Response
- **Severity:** High
- **Location:** /my-account?id=
- **Tool Used:** Burp Suite Repeater

## 2. Description
The application attempts to prevent unauthorized access
to other users' accounts by returning a 302 Redirect.
However, sensitive user data including the API Key is
still included in the response body before the redirect
occurs. An attacker can intercept the 302 response in
Burp Suite and read the sensitive data before the
browser follows the redirect.

## 3. Steps to Reproduce
1. Login as wiener:peter
2. Intercept requests in Burp Suite
3. Navigate to /my-account?id=carlos
4. Application returns 302 Redirect
5. Intercept the response in Burp before redirect
6. Read the response body — carlos API Key is exposed
7. Copy the API Key and submit as solution

## 4. Evidence
 <img width="1919" height="1011" alt="Screenshot 2026-08-03 104118" src="https://github.com/user-attachments/assets/49d1af71-84eb-4596-99a2-f15e3ce1f1d1" />


## 5. Impact
An attacker can access sensitive data of any user
despite the redirect protection. The redirect only
affects the browser behavior, not the server response.
All sensitive information is already transmitted before
the redirect takes effect. Full horizontal privilege
escalation across all user accounts.

## 6. Remediation
- Return an empty response body with the 302 redirect
- Enforce access control before generating the response
- Never include sensitive data in redirect responses
- Implement server-side authorization checks before
  any data is added to the response
