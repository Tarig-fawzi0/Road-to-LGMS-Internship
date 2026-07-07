# IDOR (Insecure Direct Object Reference) — Complete Write-up

> A beginner-friendly explanation of **IDOR (Insecure Direct Object Reference)** with examples, causes, impact, prevention, and a walkthrough of a typical PortSwigger lab.

---

# What is IDOR?

**IDOR** stands for **Insecure Direct Object Reference**.

Breaking down the name:

* **Insecure** → Not properly protected
* **Direct** → The application directly references an object
* **Object Reference** → Any resource stored by the application (user account, file, image, invoice, order, etc.)

An IDOR vulnerability occurs when an application exposes a direct reference to an object **without verifying whether the current user is authorized to access it**.

Instead of checking ownership, the application simply trusts the identifier supplied by the user.

---

# The Core Concept

Every object inside an application usually has an identifier.

Examples:

```text
User Profile
/users/123

Invoice
/invoices/INV-2026-001

Image
/images/photo15.jpg

File
/files/2.txt

Order
/api/orders/4589
```

Normally:

```
User
      ↓
Requests object
      ↓
Server verifies ownership
      ↓
Returns data
```

In an IDOR vulnerability:

```
User
      ↓
Changes object ID
      ↓
Server trusts the request
      ↓
Returns another user's data ❌
```

---

# Types of IDOR

## 1. IDOR in URL Parameters

Example:

```
GET /my-account?id=123
```

Changing the ID:

```
GET /my-account?id=124
```

If another user's account appears, the application is vulnerable.

---

## 2. IDOR in File Access

Example:

```
/files/2.txt
```

Change it to:

```
/files/1.txt
```

If another user's file is displayed, this is an IDOR vulnerability.

---

## 3. IDOR in APIs

Example:

```
GET /api/orders/555
```

Modify it:

```
GET /api/orders/554
```

If another customer's order is returned, authorization is missing.

---

## 4. IDOR in POST Requests

Example:

```http
POST /transfer

{
    "from_account":"123",
    "to_account":"456",
    "amount":"100"
}
```

Changing:

```json
{
    "from_account":"999",
    "to_account":"456",
    "amount":"100"
}
```

If the server processes the transfer from another user's account, it is vulnerable.

---

## 5. IDOR in Hidden Form Fields

HTML:

```html
<input type="hidden" name="user_id" value="123">
```

Changing it to:

```html
<input type="hidden" name="user_id" value="124">
```

may allow actions on another user's account.

---

# Why Does IDOR Happen?

The root cause is **missing authorization**.

The application trusts user input instead of verifying ownership.

Example:

```
Client:
id=5

Server:
"Okay, here's object #5."
```

What should happen:

```
Client:
id=5

Server:
Does object #5 belong to this user?

Yes → Allow

No → Deny access
```

---

# Common Causes

## 1. Trusting User Input

The application assumes the supplied ID is valid.

```
?id=5

↓

Return record #5
```

No ownership check is performed.

---

## 2. Predictable Object IDs

Sequential IDs are easy to guess.

```
User A
/files/1.txt

User B
/files/2.txt

User C
/files/3.txt
```

Attackers simply enumerate them.

---

## 3. Missing Authorization

Many developers implement authentication but forget authorization.

---

# Authentication vs Authorization

These two concepts are often confused.

## Authentication

Answers:

> Who are you?

Example:

```
Username:
wiener

Password:
peter
```

Result:

```
✓ Logged in
```

---

## Authorization

Answers:

> What are you allowed to access?

Example:

```
Logged in as:

wiener
```

Trying to access:

```
/files/1.txt
```

Server checks:

```
Does this file belong to wiener?

No

↓

Access Denied
```

If this check is missing, IDOR exists.

---

# Real-World Example

Imagine an online banking application.

```
Your account:

10001
```

Request:

```
GET /account?id=10001
```

Changing it to:

```
GET /account?id=10002
```

If another customer's bank account appears, the application suffers from IDOR.

---

# Typical PortSwigger Lab Walkthrough

Scenario:

The application stores chat history as text files.

Logged in as:

```
wiener
```

You download your chat log.

URL:

```
/download-transcript/2.txt
```

Observation:

```
My transcript is:

2.txt
```

Since IDs are sequential, it's reasonable to test:

```
1.txt
```

Request:

```
GET /download-transcript/1.txt
```

The server returns another user's chat log.

Inside the chat log:

```
Username:
carlos

Password:
********
```

Use Carlos's credentials to log in.

The lab is solved.

---

# Why Is IDOR Dangerous?

IDOR is considered one of the most dangerous web vulnerabilities because it can expose sensitive information without requiring sophisticated exploitation.

An attacker may gain access to:

* Personal information
* Financial records
* Medical records
* Orders
* Uploaded files
* Internal documents
* Private messages
* Password reset tokens
* Administrative functionality

Sometimes changing **one number** is enough to compromise thousands of users.

---

# How to Prevent IDOR

## 1. Always Verify Ownership

Never trust object identifiers provided by the client.

Incorrect:

```php
return file_get_contents($id);
```

Correct:

```php
if(fileBelongsToUser($id, $currentUser)){
    return file_get_contents($id);
}

return "Access Denied";
```

---

## 2. Perform Authorization on Every Request

Every endpoint should verify permissions.

Example:

```
GET /profile

✓ Verify owner

GET /invoice

✓ Verify owner

GET /files

✓ Verify owner

DELETE /order

✓ Verify owner
```

---

## 3. Avoid Predictable IDs

Instead of:

```
1
2
3
4
5
```

Use UUIDs.

Example:

```
550e8400-e29b-41d4-a716-446655440000
```

Although UUIDs do **not replace authorization**, they make object enumeration significantly harder.

---

## 4. Enforce Server-Side Authorization

Never rely on:

* Hidden fields
* JavaScript
* Client-side checks

All authorization decisions must happen on the server.

---

## 5. Apply Least Privilege

Users should only access resources they own or are explicitly permitted to use.

---

# Testing Checklist

When testing for IDOR, ask yourself:

* Can I change an ID in the URL?
* Can I modify an API endpoint?
* Can I edit hidden form fields?
* Can I alter JSON values?
* Can I access another user's files?
* Are IDs sequential?
* Does the server verify ownership?
* Can I enumerate resources by changing numbers?

---

# Key Takeaways

* **IDOR = Missing authorization, not missing authentication.**
* Logging in does **not** mean you should access every object.
* The server must always verify ownership before returning data.
* Sequential identifiers make exploitation easier but are **not** the root cause.
* Proper server-side authorization is the real defense.

---

# Summary

| Concept        | Description                                                               |
| -------------- | ------------------------------------------------------------------------- |
| Vulnerability  | Insecure Direct Object Reference (IDOR)                                   |
| OWASP Category | Broken Access Control (OWASP Top 10 #1)                                   |
| Root Cause     | Missing authorization checks                                              |
| Typical Attack | Change an object identifier (ID, filename, UUID, order number, etc.)      |
| Common Targets | Files, profiles, invoices, APIs, orders, images                           |
| Impact         | Unauthorized access to sensitive data                                     |
| Prevention     | Validate ownership and enforce server-side authorization on every request |

 
 
 
