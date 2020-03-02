| Secure Communications – Mark Cummins – TUDublin | 
| ------ | 
|These notes and exercises are part of the Secure Communications module on the Digital Forensics and Cyber Security course at Technological University Dublin. |




## Lab 5B: Breaking Salted Hashes

In the previous lab we looked at various different approaches to password hashing. In this challenge lab we'll play the role of the hacker attempting to brute-force a captured database of user credentials including salted hashes of the user's passwords. The lab will involve brute forcing and may take several hours to complete fully. So if you have a spare machine you can leave running then that might be an option or if you're feeling adventurous maybe look at running your brute forcing on some cloud setup (but watch the costs!!!)

Whatever your approach I strongly suggest you invest your time wisely in completely understanding your tool of choice before wasting time running searches only to realise you've done it wrong and have to run again, and again. 

___


### 1. Pick your weapon

You can try scripting your own solution or using a brute forcing tool designed for just such a job, there are plenty to pick from so choose wisely. Personally I'd recommend using Hashcat, but it has a bit of a steep learning curve when just getting starting, but it's time well invested. Here's a [quick tutorial](https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-3-using-hashcat-0156543/) that might help.


### 2. Challenge Details

You’ve been asked by the Garda to assist in helping to retrieve some hashed passwords. They have managed to get a dump of one of the database tables, however they still need the original passwords and have been unable to crack them themselves and have called in your help.

The issue seems to be that the database is only storing the password hashes, and so far their attempts to brute force the passwords have failed. They have tried their standard rainbow tables without success and suspect that the passwords may have been salted. 

A brief analysis of the hashes supports this belief and indicates that all the passwords have been hashed with the same salt.Can you help the Garda and crack any of the salted hashed passwords?


**Some potentially useful information from the Garda case files:**

- The password policy file was changed in May 2019, passwords created after this date are alphanumeric 5-7 characters in length. Passwords created before these dates are believed to have consisted of only digits and 5-7 characters in length.
- It’s believed that all passwords have used the same salt, however the salt is missing from the database and all source code has been corrupted.
- The salt is believed to be a short (5 digits) numerical string
- The database dump is from MySQL database
- Some of the captured source code from the site, reveals the salt format as CommonHash($salt,$pass)

Retrieve as much information as you can from the dump below for the Garda

| Join_date | Username | Password | Role | Last_accessed | Pass_modified |
| --------- | -------- | -------- | ---- | ------------- | ------------- |
|2018-06-07|Sparky|c277243d2d39de474f3070d5c673ed492cea1b9e|Admin|2020-02-25|2020-01-09|
|2019-06-03|Mark123|7a1d64ffa965a52b420570aa4f4c6aa450870fea|user|2019-12-20|2019-06-03|
|2018-09-02|superman|3450fd71d9702d3a7b835a1536a9ad2650eff209|user|2020-01-12|2019-10-01|
|2019-01-11|security|0f295b9e67f362f1be3cd7d0b30d4f4007f88a0e|user|2019-12-07|2019-04-11|
|2018-12-03|Tomtom|d71b12c1eb8bf31ca6d19344e2504b0d2916635e|user|2019-12-03|2018-01-03|
|2019-04-11|JillC|335bcd081c21b75a3866262fc45545c880786054|user|2020-02-19|2019-12-20|


### 5. Submission

You just need to upload your final user:password pairs for any of the hashes that you managed to brute force and then demo your approach during the labs.
