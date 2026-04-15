# My Pentesting Cheatsheet

## Nmap
nmap -sV -sC 10.x.x.x        ← default scan, top 1000 ports

nmap -p- -sV 10.x.x.x        ← full port scan, all 65535 ports

nmap -p- --min-rate 5000      ← faster full scan

## SMB
smbclient -L 10.x.x.x        ← list shares

smbclient \\\\ip\\share       ← connect to share

## Redis
redis-cli -h 10.x.x.x        ← connect

keys *                        ← list all keys

get <keyname>                 ← retrieve value
