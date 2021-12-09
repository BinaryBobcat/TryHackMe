# Advent of Cyber 3 (2021)

> Dec. 1, 2021

## [Day 6] Web Exploitation Patch Management Is Hard

**What is the risk of LFI?**

Once you find an LFI vulnerability, it is possible to read sensitive data if you have readable permissions on files. Thus, one of the most significant risks is leaking sensitive data accessed by a regular user. Also, in some cases, an LFI vulnerability could be chained to perform Remote Code Execution RCE on the server. If we can inject or write to a file on the system, we take advantage of LFI to get RCE. In this task, we prepared a web application with an LFI vulnerability and a possible way to get RCE. We'll be looking at this web application later.

![](screenshots/AOC3_day6-0.png)

1. Deploy the attached VM and look around. What is the entry point for our web application? 

hxxp://10.10.132.188/index.php?err=/etc/passwd

`Answer: err`

2. Use the entry point to perform LFI to read the /etc/flag file. What is the flag?

hxxp://10.10.132.188/index.php?err=/etc/flag

`Answer: THM{d29e08941cf7fe41df55f1a7da6c4c06} `

3. Use the PHP filter technique to read the source code of the index.php. What is the $flag variable's value?

hxxp://10.10.132.188/index.php?err=php://filter/convert.base64-encode/resource=index.php

![](screenshots/AOC3_day6-3.png)

`Answer: THM{791d43d46018a0d89361dbf60d5d9eb8}`

4. *McSkidy forgot his login credential. Can you help him to login in order to recover one of the server's passwords?* Now that you read the index.php, there is a login credential PHP file's path. Use the PHP filter technique to read its content. What are the username and password?

hxxp://10.10.132.188/index.php?err=php://filter/convert.base64-encode/resource=./includes/creds.php

![](screenshots/AOC3_day6-4.png)

`Answer: McSkidy:A0C315Aw3s0m`

5. Use the credentials to login into the web application. Help McSkidy to recover the server's password. What is the password of the flag.thm.aoc server? 

Navigate to Password Recovery tab.

`Answer: THM{552f313b52e3c3dbf5257d8c6db7f6f1}`

6. The web application logs all users' requests, and only authorized users can read the log file. Use the LFI to gain RCE via the log file page. What is the hostname of the webserver? The log file location is at ./includes/logs/app_access.log.

**LFI to RCE via Log files**

It is also called a log poisoning attack. It is a technique used to gain remote command execution on the webserver. The attacker needs to include a malicious payload into services log files such as Apache, SSH, etc. Then, the LFI vulnerability is used to request the page that includes the malicious payload. Exploiting this kind of attack depends on various factors, including the design of the web application and server configurations. Thus, it requires enumerations, analysis, and an understanding of how the web application works. For example, a user can include a malicious payload into an apache log file via User-Agent or other HTTP headers. In SSH, the user can inject a malicious payload in the username section. 

The User-Agent is one of the HTTP headers that the user can control. Therefore, in order to get the RCE, you need to include PHP code into User-Agent and send a request to the log file using the LFI to execute in the browser. 

Test:
`curl -A "This is testing" http://10.10.132.188/login.php`

Code Execution can be done sending a php payload. 

`Answer: lfi-aoc-awesome-59aedca683fff9261263bb084880c965`

7. **Bonus:** The current PHP configuration stores the PHP session files in /tmp. Use the LFI to call the PHP session file to get your PHP code executed.