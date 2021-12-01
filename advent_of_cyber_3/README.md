# Advent of Cyber 3 (2021)

> Dec. 1, 2021

## [Day 1] Web Exploitation Save The Gifts 

1. After finding Santa's account, what is their position in the company?

        Change the query component value for id to 1. 

        Answer: The Boss!

2. After finding McStocker's account, what is their position in the company?

        Change the query component value for id to 3. 

        Answer: Build Manager

3. After finding the account responsible for tampering, what is their position in the company?

        Change the query component value for id to 9. The data shows multiple inventory sku changes.

        Answer: Mischief Manager

4. What is the received flag when McSkidy fixes the Inventory Management System?

        Navigate to id 9 and revert all inventory.

        Answer: THM{AOC_IDOR_2B34BHI3}
