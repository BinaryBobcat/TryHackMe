# Advent of Cyber 3 (2021)

> Dec. 1, 2021

## [Day 3] Web Exploitation Christmas Blackout 

1. Using a common wordlist for discovering content, enumerate hxxp://10.10.210.162/ to find the location of the administrator dashboard. What is the name of the folder? 

Enumerating the domain can be done using the Seclist. 
https://github.com/danielmiessler/SecLists 

`$ dirb hxxp://10.10.210.162/ /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt`

`Answer: admin`

![](../screenshots/AOC3_day3-1.png)

2. In your web browser, try some default credentials on the newly discovered login form for the "administrator" user. What is the password?

Simple guessing of common passwords.

`Answer: administrator`

3. Access the admin panel. What is the value of the flag?

`Answer: THM{ADM1N_AC3SS}`