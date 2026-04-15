# Fawn — HackTheBox

**Difficulty:** Very Easy  
**Category:** Starting Point / Tier 0  
**Date:** April 2026

## Summary
Exploited an FTP service that allowed anonymous login 
to retrieve the flag.

## Enumeration
I started by scanning the target using Nmap:

nmap -sC -sV 10.129.114.42

The scan showed:

 Port 21/tcp open — FTP (vsftpd 3.0.3)
 Nmap noted anonymous login allowed

## Exploitation
Connected to FTP using anonymous credentials.

ftp 10.129.114.42

Username: anonymous
Password: (blank / just hit enter)
Successfully logged in

Listed files and downloaded the flag.

ls
get flag.txt

## What I Learned
- How FTP works and common misconfigurations
- Anonymous FTP login as an attack vector
- Basic FTP commands (ls, get, cd)
- Why anonymous access should always be 
  disabled on production servers
