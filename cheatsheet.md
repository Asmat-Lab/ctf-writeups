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

## Password Cracking (John the Ripper)

**Crack with RockYou:**
    ```
    john --wordlist=/usr/share/wordlists/rockyou.txt <file name>
    ```
*   **Check Already Cracked Passwords:**
    ```
    john --show <file name>
    ```
*   **Extract Zip Hash:**
    ```
    zip2john secret.zip > <file name>
     ```
    
    ##  Remote Access & Shells
    
*   **Evil-WinRM:** (Windows management shell)
    ```bash
    evil-winrm -i 10.x.x.x -u username -p 'password'
    ```
*   **SSH:** (Linux access)
    ```bash
    ssh username@10.x.x.x
    ```

    ## Web Enumeration
*   **Directory Brute-forcing:** (Find hidden folders)
    ```bash
    gobuster dir -u http://10.x.x.x -w /usr/share/wordlists/dirb/common.txt
    ```
