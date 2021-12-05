# Advent of Cyber 3 (2021)

> Dec. 1, 2021

## [Day 1] Web Exploitation Save The Gifts 

1. After finding Santa's account, what is their position in the company?

Change the query component value for id to 1. 

`Answer: The Boss!`

2. After finding McStocker's account, what is their position in the company?

Change the query component value for id to 3. 

`Answer: Build Manager`

3. After finding the account responsible for tampering, what is their position in the company?

Change the query component value for id to 9. The data shows multiple inventory sku changes.

`Answer: Mischief Manager`

4. What is the received flag when McSkidy fixes the Inventory Management System?

Navigate to id 9, and revert all inventory.

`Answer: THM{AOC_IDOR_2B34BHI3}`

---

## [Day 2] Web Exploitation Elf HR Problems 

Open the static site in a new tab.

Register an account, and verify the cookies using the Developer Tools in your browser.

1. What is the name of the new cookie that was created for your account?

Press F12, click "Sign Up" and provide dummy information. Click your cookies under storage.

`Answer: user-auth `

2. What encoding type was used for the cookie value?

Cyberchef is a great tool for encoding/decoding values. If you could not determine by eye, you can use the "magic" feature in cyberchef. 

`Answer: hexadecimal`

3. What object format is the data of the cookie stored in?

After decoding the cookie value, the object format is json. 

`Answer: json`

Manipulate the cookie and bypass the login portal.

4. What is the value of the administrator cookie? (username = admin)

In cyberchef, copy the decoded value from our cookie. Edit the username value to admin. Convert back to hex.

`Answer: 7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a2261646d696e227d`

![](screenshots/AOC3_day2-4.png)

5. What team environment is not responding?
        
`Answer: HR`

![](screenshots/AOC3_day2-5.png)

6. What team environment has a network warning?

`Answer: Application`

---

## [Day 3] Web Exploitation Christmas Blackout 

1. Using a common wordlist for discovering content, enumerate hxxp://10.10.210.162/ to find the location of the administrator dashboard. What is the name of the folder? 

Enumerating the domain can be done using the Seclist. 
https://github.com/danielmiessler/SecLists 

`$ dirb hxxp://10.10.210.162/ /opt/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt`

`Answer: admin`

![](screenshots/AOC3_day3-1.png)

2. In your web browser, try some default credentials on the newly discovered login form for the "administrator" user. What is the password?

Simple guessing of common passwords.

`Answer: administrator`

3. Access the admin panel. What is the value of the flag?

`Answer: THM{ADM1N_AC3SS}`

---

## [Day 4] Web Exploitation Santa's Running Behind

1. What valid password can you use to access the "santa" account?

In burpsuite we will turn intercept on, navigate to the target IP, put in our credentials user: `santa` password:`test` and before clicking login, turn our FoxyProxy on in our browser. After that, we can click login and navigate back to burpsuite. Once in burpsuite we can right-click the intercepted data and send it to intruder, clear all for positions, add the password parameter as the only position, set the attack type to sniper, and navigate to payloads. Download the provided payload and load the document. Start the attack! :)

`Answer: cookie`

![](screenshots/AOC3_day4-1.png)

2. What is the flag in Santa's itinerary?

Applying our newly found password `cookie,` we can login. 

`Answer: THM{SANTA_DELIVERS}`

![](screenshots/AOC3_day4-2.png)

---

## [Day 5] Web Exploitation Pesky Elf Forum 

1. What flag did you get when you disabled the plugin?

Guided walkthrough of XSS. 

`Answer: THM{NO_MORE_BUTTMAS}`

---