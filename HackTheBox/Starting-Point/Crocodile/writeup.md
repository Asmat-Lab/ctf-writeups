# Crocodile — HackTheBox Starting Point

**Difficulty:** Very Easy
**Tier:** 1
**Date:** April 2026


## Summary
Used anonymous FTP access to find credential files,
then used those credentials to log into a web admin
panel and retrieve the flag.

## Enumeration
nmap -sV -sC 10.129.124.97

**Results:**
- Port 21/tcp open — FTP (vsftpd 3.0.3)
- Port 80/tcp open — HTTP (Apache httpd 2.4.41)
- Nmap noted anonymous FTP login allowed

Two services running — checked FTP first since
anonymous access was flagged.

## Exploitation
Connected to FTP anonymously and enumerated files.

ftp 10.129.124.97

Username: anonymous

Password: (blank)

ls

Found two interesting files.

get allowed.userlist

get allowed.userlist.passwd

Downloaded both files and read them locally.

cat allowed.userlist

cat allowed.userlist.passwd

Files contained a list of usernames and passwords
in plaintext.

Navigated to the web application on port 80.
Found a standard HTML page — directory busted
for hidden pages.

gobuster dir -u http://10.129.124.97 -w
/usr/share/wordlists/dirb/common.txt

Found /login.php admin panel. Tried credential
combinations from the FTP files.

username: admin 

password: rKXM59ESxesUFHAd

Logged in and retrieved the flag.

## Flags
- Root flag: c7110277ac44d78b6a9fff2232434d16

## What I Learned
- How to chain two services together in one attack path
- Anonymous FTP can expose sensitive files like
  credential lists — a serious real-world misconfiguration
- Directory busting with Gobuster to find hidden pages
- The importance of checking ALL services found,
  not just the obvious ones
- Credential stuffing from discovered files into
  other services on the same target
