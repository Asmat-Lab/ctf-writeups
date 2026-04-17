# Sequel — HackTheBox Starting Point

**Difficulty:** Very Easy

**Tier:** 1

**Date:** April 2026

## Summary
Connected to an exposed MySQL database using default
credentials and enumerated tables to find the flag.

## Enumeration
nmap -sV -sC 10.129.118.140

**Results:**
- Port 3306/tcp open — MySQL

MySQL is running directly accessible on the network.

## Exploitation
Attempted to connect to MySQL with common default
credentials. Root with no password worked.

mysql -h 10.129.118.140 -u root

Once inside, enumerated available databases and
tables systematically.

show databases;

Four databases were shown, and then I used the keyword " use " to interact with the htb database.

use htb;

Once inside the htb database, I searched for the tables using:

show tables;

The table displayed "config" and "users."

I ran the select * from command on both, and I ended up finding the flag
in config.

SELECT * from config;

## Flags
- Root flag: 7b4bec00d1a39e3dd4e021ec3d915da8



## What I Learned
- How MySQL works and basic SQL query syntax
- Why databases should never be directly exposed
  to a network without strict access controls
- Default/empty root credentials are a critical
  misconfiguration in database services
- Key SQL commands: show databases, use, show tables,
  select * from
- How to connect to remote MySQL with mysql client
