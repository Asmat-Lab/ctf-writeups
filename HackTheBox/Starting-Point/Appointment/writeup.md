# Appointment — HackTheBox Starting Point

**Difficulty:** Very Easy  
**Category:** Starting Point / Tier 1  
**Date:** April 2026

## Summary
Exploited a login form vulnerable to SQL injection
to bypass authentication and retrieve the flag.

## Enumeration
Started with an Nmap scan to identify open ports and services.

nmap -sV -sC 10.129.117.226

**Results:**
- Port 80/tcp open — HTTP Apache httpd 2.4.38 ((Debian))

Navigated to the web application in browser. 
Found a login page with username and password fields.



## Exploitation
Attempted SQL injection on the login form to bypass
authentication without knowing valid credentials.

Tested the classic authentication bypass payload
in the username field.

Username: admin'#

Password: (anything)

The # character comments out the rest of the SQL
query after the username, making the password
check irrelevant.

Successfully logged in and retrieved the flag.



## What I Learned
- How SQL injection works at a basic level
- How # comments out SQL code in MySQL queries
- Why parameterized queries / prepared statements
  prevent this attack entirely
- How to test login forms for SQLi manually

