# Advent of Cyber 3 (2021)

> Dec. 1, 2021

## [Day 4] Web Exploitation Santa's Running Behind

1. What valid password can you use to access the "santa" account?

In burpsuite we will turn intercept on, navigate to the target IP, put in our credentials user: `santa` password:`test` and before clicking login, turn our FoxyProxy on in our browser. After that, we can click login and navigate back to burpsuite. Once in burpsuite we can right-click the intercepted data and send it to intruder, clear all for positions, add the password parameter as the only position, set the attack type to sniper, and navigate to payloads. Download the provided payload and load the document. Start the attack! :)

`Answer: cookie`

![](screenshots/AOC3_day4-1.png)

2. What is the flag in Santa's itinerary?

Applying our newly found password `cookie,` we can login. 

`Answer: THM{SANTA_DELIVERS}`

![](screenshots/AOC3_day4-2.png)