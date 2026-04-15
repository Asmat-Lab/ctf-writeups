# My Pentesting Cheatsheet

---

## Network Scanning (Nmap)

# Default scan (scripts + service detection)
nmap -sC -sV <target-ip>

# Full port scan (all TCP ports)
nmap -p- <target-ip>

# Fast full port scan
nmap -p- --min-rate 5000 <target-ip>

---

## Telnet (Telecommunication Network Protocol)

# Connect to Telnet service
telnet <target-ip>

---

## File Transfer Protocol (FTP)

# Connect to FTP service
ftp <target-ip>

# List files on remote server
ls

# Download file from server
get <filename>

---

## Server Message Block (SMB Protocol)

# List available shares
smbclient -L <target-ip>

# Connect to a specific share
smbclient //<target-ip>/<share>

# List files inside share
ls

# Download file from share
get <filename>

---

## Redis (Remote Dictionary Server)

# Connect to Redis service
redis-cli -h <target-ip>

# List all stored keys
keys *

# Retrieve value from key
get <keyname>
