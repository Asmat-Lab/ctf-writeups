# Meow — HackTheBox

**Difficulty:** Very Easy  
**Category:** Starting Point / Tier 0  
**Date:** April 2026

## Overview
- Goal: Gain access to the system and retrieve the flag
  
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
- Basic service enumeration with Nmap
- How Telnet works and why it's insecure
- Default credential attacks
