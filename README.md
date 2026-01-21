# SQL Injection Penetration Test Report
## PortSwigger SQL injection vulnerability allowing login bypass

**Prepared by:** Elroy Fernandes    
**Date:** January 21, 2026  
**Environment:** Kali Linux (Local Install)  
**Target:** PortSwigger Lab: SQL injection vulnerability allowing login bypass 
**Test Type:** Ethical Hacking - SQL Injection Assessment

---

## Executive Summary

This report documents a successfull SQL injection attack against the PortSwigger login page conducted in a controlled, local environment. The vulnerability allowed authentication bypass using a simple SQLi payload (`' OR 1=1 --`), granting unauthorized administrative access. 
This assessment was performed for educational purposes to demonstrate common web application vulnerabilities and remediation strategies.

**Key Finding:** High-severity SQL Injection (CWE-89) on login functionality  
**Impact:** Complete authentication bypass, full admin privileges  
**Status:** Proof of Concept Achieved

## 1. Scope and Objectives

### Scope
- **Application:** PortSwigger Lab (intentionally vulnerable web application)
- **Environment:** Local Kali Linux deployment
- **Target Component:** User login page
- **Testing Method:** Manual penetration testing

### Objectives
- Identify and exploit authentication vulnerabilities
- Demonstrate SQL injection techniques
- Document findings and remediation steps
- Showcase ethical security testing methodology

---

## 2. Technical Finding: SQL Injection (Authentication Bypass)

### Description

The login form does not use parameterized queries or prepared statements when
validating user credentials. By injecting SQL syntax into the username field,
an attacker can manipulate the backend query logic to always evaluate as true,
resulting in authentication bypass.

---

## Steps to Reproduce (Proof of Concept)

### Step 1: Click on My account
<p aligh="center">
	<img src="screenshots/HomePage.png" alt="PortSwigger HomePage"
	width="60%">
</p>

<p align="center">
	<img src="screenshots/loginPage.png" alt="PortSwigger Login Page" 
	width="60%">
</p>

### Step 2: Inject SQL Payload

Enter the following payload into the Email/Username field:

```sql
admin' OR 1=1--
```
<p align="center">
	<img src="screenshots/sqlpayload.png" alt="SQL Payload"
	width="60%"
</p>

### Step 3: Enter any arbitrary string in the Password field (e.g: SomethingPassword1)
### Step 4: Click Login
### Step 5: Result
The website proccess the query, ignores the password check due to the comment operator (--), and authenticates the user as the administrator.

