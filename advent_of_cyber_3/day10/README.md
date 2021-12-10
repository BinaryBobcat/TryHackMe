# Advent of Cyber 3 (2021)

> Dec. 10, 2021

## [Day 10] Networking Offensive Is The Best Defence 

1. Help McSkidy and run nmap -sT MACHINE_IP. How many ports are open between 1 and 100? 



`Answer: `

2. What is the smallest port number that is open?



`Answer: `

3. What is the service related to the highest port number you found in the first question?



`Answer: `

4. Now run nmap -sS MACHINE_IP. Did you get the same results? (Y/N)



`Answer: `

5. If you want Nmap to detect the version info of the services installed, you can use nmap -sV MACHINE_IP. What is the version number of the web server?



`Answer: `

6. By checking the vulnerabilities related to the installed web server, you learn that there is a critical vulnerability that allows path traversal and remote code execution. Now you can tell McSkidy that Grinch Enterprises used this vulnerability. What is the CVE number of the vulnerability that was solved in version 2.4.51?



`Answer: `

7. You are putting the pieces together and have a good idea of how your web server was exploited. McSkidy is suspicious that the attacker might have installed a backdoor. She asks you to check if there is some service listening on an uncommon port, i.e. outside the 1000 common ports that Nmap scans by default. She explains that adding -p1-65535 or -p- will scan all 65,535 TCP ports instead of only scanning the 1000 most common ports. What is the port number that appeared in the results now?



`Answer: `

8. What is the name of the program listening on the newly discovered port?



`Answer: `
