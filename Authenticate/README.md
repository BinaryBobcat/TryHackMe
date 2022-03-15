# Authenticate

Learn how to attack authentication mechanisms used in web applications
# TryHackMe - Authenticate

## Task 1  Deploy the VM

###  - Deploy the VM

## Task 2  Dictionary attack

###  - What is the flag you found after logging as Jack?

`fad9ddc1feebd9e9bca05f02dd89e271`

###  - Now try the same thing for username mike.

###  - What is the flag you found after logging as Mike?

hydra -l mike -P /usr/share/wordlists/rockyou.txt 10.10.226.198 -s 8888 http-post-form "/login:user=mike&password=^PASS^:Invalid username or password"

`e1faaa144df2f24aa0a9284f4a5bb578`

## Task 3  Re-registration

###  - What is the flag that you found in darren's account?

`fe86079416a21a3c99937fea8874b667`

###  - Now try to do the same trick and see if you can login as arthur.

###  - What is the flag that you found in arthur's account?

`d9ac0f7db4fda460ac3edeb75d75e16e`

## Task 4  JSON Web Token

###  - Use the same method to find identity of admin user and retrieve the flag?

Capture the JWT token. Decode each section of the JWT individually. Remember when encoding to add a new line after each json {}. Leave the signature blank and forward. 

`92498880383088033228`

## Task 5  No Auth

###  - Find the way to get into superadmin ad

Login as admin. Navigate to the 0 url once logged in. 

###  - What is the password for superadmin account?

`abcd1234`

###  - What is the flag you found in superadmin account?

`72102933396288983011`
