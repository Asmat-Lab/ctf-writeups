# My Pentesting Cheatsheet

## Nmap
*   **Default Scan:** (Top 1000 ports, service versions, default scripts)
    ```bash
    nmap -sV -sC 10.x.x.x
    ```
*   **Full Port Scan:** (All 65,535 ports)
    ```bash
    nmap -p- -sV 10.x.x.x
    ```
*   **Fast Full Scan:** (Aggressive rate to save time)
    ```bash
    nmap -p- --min-rate 5000 10.x.x.x
    ```

## SMB
*   **List Shares (Anonymous):**
    ```bash
    smbclient -L //10.x.x.x/ -N
    ```
*   **Connect to Share:**
    ```bash
    smbclient //10.x.x.x/sharename -U username
    ```

## Redis
*   **Connect:**
    ```bash
    redis-cli -h 10.x.x.x
    ```
*   **Basic Commands:**
    ```bash
    keys *        # List all keys
    get <key>     # View value of a key
    info          # Show server info
    ```

## Password Cracking (John the Ripper)

*   **Crack with RockYou:**
    ```bash
    john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
    ```
*   **Check Already Cracked Passwords:**
    ```bash
    john --show hash.txt
    ```
*   **Extract Zip Hash:**
    ```bash
    zip2john secret.zip > hash.txt
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
