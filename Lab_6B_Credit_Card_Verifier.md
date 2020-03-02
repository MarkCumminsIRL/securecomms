| Secure Communications – Mark Cummins – TUDublin | 
| ------ | 
|These notes and exercises are part of the Secure Communications module on the Digital Forensics and Cyber Security course at Technological University Dublin. |

## Lab 6B: Python Challenge - Credit Card Verifier

Hashes and checksums, can be found everywhere in modern database and software systems and everyday life. Credit cards are part of our everyday life, most people have at least one, and we use them to pay for goods and services in both the physical and online worlds.

Credit cards and bank cards are no strangers to checksums. Your task for this challenge is to research the checksum function used for credit cards (Luhn) and to implement the algorithm so that you can check credit card numbers yourself and verify if they are
valid.
___

You're program should have a number of modes:  

1. **Verify:** Take a credit card number as input and output if it is a valid or invalid credit card number.
2. **Vendor:** Again take a credit card number as input and output the issuing vendor
3. **Checksum:** Given just the first portion of a credit card calculate the checksum (Calculate last four digits)
4. **Generate:** Select the issuing vendor from a list, then generate a random valid credit card for that vendor.

You may also want to look at the [vendor numbers for each card](https://en.wikipedia.org/wiki/Payment_card_number)

___


### Submission
You should submit your final python code to solve the challenge. You'll be asked to show your code on github and demo and explain it working during the lab.





