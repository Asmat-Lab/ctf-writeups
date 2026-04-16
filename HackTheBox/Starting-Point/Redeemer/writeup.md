# Redeemer — HackTheBox Starting Point

**Difficulty:** Very Easy  
**Category:** Starting Point / Tier 0  
**Date:** April 2026

## Summary
Connected to an exposed Redis instance with no 
authentication configured and retrieved the flag 
directly from the database.

## Enumeration
Started with a standard Nmap scan.

nmap -sV -sC 10.129.114.205

No open ports returned. Realized the service might
be running on a non-default port so ran a full
port scan across all 65535 ports.

nmap -p- -sV 10.129.114.205

**Results:**
- Port 6379/tcp open — Redis key-value store

Key lesson: default Nmap only scans top 1000 ports.
Always follow up with -p- if initial results look empty
or suspicious.

## Exploitation
Redis-cli was not installed by default on my system.
Installed it first.

sudo apt install redis-tools

Connected to the Redis instance with no password required.

redis-cli -h 10.129.114.205

Ran basic Redis commands to enumerate the database
and find the flag.

info          ← get server info and keyspace
select 0      ← select database 0
keys *        ← list all keys
get flag      ← retrieve the flag value



## What I Learned
- What Redis is and what it's used for in real applications
- Why Redis should never be exposed to the internet 
  without authentication
- Basic Redis CLI commands (info, select, keys, get)
- The importance of scanning all ports, not just 
  common ones — Redis on 6379 would be missed 
  by a default Nmap scan
- Why -p- flag matters for thorough enumeration
