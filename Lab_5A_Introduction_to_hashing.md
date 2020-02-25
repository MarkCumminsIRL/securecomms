| Secure Communications – Mark Cummins – TUDublin | 
| ------ | 
|These notes and exercises are part of the Secure Communications module on the Digital Forensics and Cyber Security course at Technological University Dublin. |




## Lab 5: Hashing Lab (pt 1) – Hash That Password

The learning objective of this lab is for students to get familiar with the concepts of creating and checking basic file hashes. Students will gain first-hand experience creating and verifying file hashes. Students will also learn how to properly save passwords and investigate how hackers typically attack databases of badly hashed passwords.

___

### Lab Contents

1. Lab Environment
2. Lab Tasks
    1. Investigating Basic Hashing
    2. Investigating File Hashing
    3. Investigating Hash collisions
    4. Making a Hash of Password Security
    5. Rainbow Tables
    6. Salted Hashes
    7. Crypto currencies are to blame!
3. Submission


___

### 1. Lab Environment

All labs have been tested and designed to use Kali Linux 2020.1, however most modern Linux distro should be very similar

### 2. Lab Tasks

#### 2.1 Investigating Basic Hashing
Let's start by introducing the built in command line tools `md5sum` and `shasum`. Open up your own terminal and try calculating the both the MD5 and SHA1 hash for the string 'Hello World' 

```bash
kali@kali:~$ echo 'Hello World' | md5sum
e59ff97941044f85df5297e1c302d260  -                    
kali@kali:~$ echo 'Hello World' | shasum                
648a6a6ffffdaa0badb23b8baf90b6168dd16b3a  - 
```

#### 2.2 Investigating File Hashing
To start this task, you should open your favorite text editor and create a file (hashme.txt) with the numbers 1 to 5 (one per line), as shown.

File: hashme.txt  
``` markdown
1  
2  
3  
4  
5  
```

Once you have created your file you should calculate the MD5 and SHA1 hash of the hashme.txt file. 

```bash
kali@kali:~$ md5sum hashme.txt
a7b1ac3a2b072f71a8e0d463bf4eb822  hashme.txt
kali@kali:~$ shasum hashme.txt
ac3b060706cf8286fc07d015ab85df7375f7b7b0  hashme.txt
```

1. What is the MD5 of the hashme.txt file?
2. What is the SHA1 of the file?
3. Are the MD5 and SHA1 hashes the same length? Explain why you think this is the case?
4. Do you think your hashes match your classmates hashes? Why?
5. Open your hashme.txt file and add a space after one of the numbers. Recalculate both the MD5 and SHA1 hashes. Have they changed much if at all from the original hashes we calculated?
6. If you changed the file name to hashme1.txt and recalculate the hashes, do you think the hashes will change? Test and see what actually happens.


#### 2.3 Investigating Hash Collisions

It has been shown that MD5, SHA1 are not collision resistant; as such both these hash functions are not suitable for applications like SSL certificates or digital signatures that rely on this property.

**Try these exercises before moving on:**
1. Read the original two papers which outlined how to attack MD5, available under the labs section on Moodle.
2. Get a copy of the two hello.exe files on Moodle and verify that their MD5 hashes match and therefore should be the same program.  
3. Now look at the contents of both files ($cat filename or you can run both programs, on windows)
4. Download the two shattered pdf files (again from Moodle) and this time verify that their SHA1 hashes are the same before opening and examining the files.
5. What do you think are the possible consequences of the two previous little tests on electronic contracts, e-commerce and digital forensic in the legal system?
6. Check out the http://shattered.io/ website and details of the attack.
7. For the two previous test cases get a different hash i.e. get the SHA1 of the good.exe and evil.exe and the MD5 of the two shattered PDF documents. Do they match now?
8. As a forensic examiner how would you go about ensuring the integrity of your assets for a legal case?


#### 2.4 Making a Hash of Password Security
When we store any user’s information in a central location we are offering any would be attackers a large target to try and attack. Why spend time trying to guess a single user’s password details etc. when we could try get the password file/database and get them all for about the same work.

There have been some very high profile leaks/hacks/robberies in recent years of large databases of user information. Some of these robberies have highlighted the need for those in charge of our data to protect it. Hashes are one way functions so even given the hashes it should be infeasible to get back the original password.

**Try these exercises before moving on:**
1. Why should we never store password as plain-text?
2. Have you ever used a password reset function that was able to tell you your original password? What does this likely mean about how they are storing passwords?
3. Outline briefly how an attacker who gets hold of the new hashed password file cannot guess the user's original password.
4. Given the hash of a password shown below can you tell which hashing algorithm was likely used to hash them? How can you tell?
`d177b4d1d9e6b6fa86521e4b3d00b029`
5. Can you figure out what password string the previous hash represents?


#### 2.5 Rainbow Tables
Great we’ve secured our new system, hashed all the passwords, our system is secure. Some hacker gets our list of user names and hashes but we can be confident that or site is still secure. Or can we?

**Try these exercises before moving on:**
1. Do a quick search on the terms **Rainbow Tables** What are they? How do they work?
2. Check out these online tools.
https://crackstation.net/
https://hashkiller.co.uk/
http://crackhash.com/
What services are they offering? How are they doing it?
3. Create the hash of one of your own commonly used passwords (or a made up one) and put the hash back into one of these on-line tools to see if it would have found your password?
4. Try googling my password hash from earlier to try cracking it. How do Google and other search engines know these hashes?
5. Check out this actual Exxon Mobil Corporation database dump by the hacking group Anonymous in Jun 2012.
http://pastebin.com/1ca3BR19
6. Are the passwords from the dump hashed? If so, which hashing algorithm was used? How can you tell?
7. Try crack a few random passwords from this actual database dump.


#### 2.6 Salted Hashes
Rainbow tables mean that normal hashed passwords are no longer secure (they haven’t been for a long time) and we shouldn’t just be storing hashed passwords in our databases. The trick is to use a salt. Basically an impurity that we add to the password before we hash it which renders the rainbow tables useless.


1. To create a salted hash we concatenate some string (the salt) to either the beginning or the end of the
password. Get the MD5 hash of the password ’qwerty’ using the salt `123123123123123`
2. Try googling the salted hash you just created to see if it can be found.
3. Do you think it would be better for a large website to use the same salt for all passwords or a different salt per password? Why?
4. Do we need to save the salt and the hash in our database or just the hash?
5. If we save the salt and hash in our database doesn’t this allow the hacker to simply break the hash again?

#### 2.7 Crypto currencies are to blame!

OK so using salted hashes is the current best practice when storing passwords in a database, but that's not quite the end of the story. Most common hash formats such as MD5 or SHA1 etc. were all chosen because of their speeds, newer algorithms can be even quicker, as all these algorithms were intended to hash large hard-disks full of data not really small passwords. 

The massive popularity of Bitcoin and other crypto currencies has also lead to the development of custom hardware optimised and designed at calculating hashes, all of which means that the cost or time to brute force salted hashes has greatly reduced in recent times.

The solution? We should use hash algorithms that have been designed with passwords in mind. These algorithms are much slower (deliberately) to discourage brute forcing. Such algorithms include Argon2 and Bcrypt2. As an exercise look them up yourself.


### 3. Submission
For this Lab you DO NOT need to submit a lab report describing what you have done or what you have observed. However you should ensure you completely understand all tasks asked of you. If you do have
any questions please don’t hesitate to ask. The goal of this lab is for you to understand all of the concepts discussed.
