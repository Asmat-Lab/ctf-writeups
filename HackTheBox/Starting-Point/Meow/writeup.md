# Meow — HackTheBox

**Difficulty:** Very Easy  
**Category:** Starting Point / Tier 0  
**Date:** April 2026

## Summary
Exploited an open Telnet service using default credentials 
to gain root access.
  
## Enumeration
I started by scanning the target using Nmap:

nmap -sC -sV 10.129.114.36

The scan showed:

Port 23 open (Telnet)

## Exploitation
Since port 23 was open, I connected using Telnet:

telnet 10.129.114.36

I tried logging in with the username:

root

No password was required, and I gained access.

After logging in, I listed the files:

ls

I found a file named `flag.txt` and displayed its contents:

cat flag.txt


## What I Learned
- How to use Nmap for basic service enumeration
- What Telnet is and why it's considered insecure 
  (credentials sent in plaintext)
- Default credential attacks as a first step 
  when finding open services
