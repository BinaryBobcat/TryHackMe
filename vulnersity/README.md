# TryHackMe - Vulnersity

> June 24, 2021

## Task 2: Reconnaissance

1. Scan the box, how many ports are open?

    Command:

	    $> nmap -sC -sV -v 10.10.161.249 -o nmap/scan

	**6 open ports:**

        21/tcp   open  ftp         vsftpd 3.0.3
        22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (
        139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
        445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
        3128/tcp open  http-proxy  Squid http proxy 3.5.12
        3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))


2. What version of the squid proxy is running on the machine?

    `3128/tcp open  http-proxy  Squid http proxy 3.5.12`

3. How many ports will nmap scan if the flag -p-400 was used?

	`400 ports`

4. Using the nmap flag -n what will it not resolve?

	`DNS`

5. What is the most likely operating system this machine is running?

	`Ubuntu`

6. What port is the web server running on?
		
	`3333/tcp open  http  Apache httpd 2.4.18 ((Ubuntu))`

## Task 3: Locating directories using GoBuster

1. What is the directory that has an upload form page?

    Command:

        $> gobuster dir -u http://10.10.161.249:3333 -w /opt/wordlist/dirbuster/directory-list-2.3-medium.txt -o gobuster/scan

    `/internal/`

## Task 4: Compromise the webserver 

1. Try upload a few file types to the server, what common extension seems to be blocked?
		
    `.php`

2. Run this attack, what extension is allowed?

    `.phtml`

3. What is the name of the user who manages the webserver?

	`bill`

4. What is the user flag?

	`8bd7992fbe8a6ad22a63361004cfcedb`

## Task 5: Privilege Escalation

1. On the system, search for all SUID files. What file stands out?

	`/bin/systemctl`

2. Become root and get the last flag (/root/root.txt)

	`a58ff8579f0a9270368d33a9966c7fd5`
