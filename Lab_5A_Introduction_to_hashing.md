# Lab 4B: Intro to Python with Pycharm

In this lab we will create our first project using the PyCharm IDE and we'll also have a quick look at finding our way around. We'll then create some basic python scripts to start our python coding.

___

## Lab Contents

1. Creating a project in PyCharm.
2. Adding our first python file.
3. Exploring the Windows
    - Run Window
    - Terminal Window
    - Python Console
4. Passing Arguments to Python
    - Using sys.argv
6. Challenge Exercise for submission.

___

### Creating a Project in PyCharm


Secure Communications and Cryptography – Mark Cummins – ITB 1
Hashing Lab 1 – Hash That Password
These notes and exercises are part of the Secure Communications and Cryptography module on the Digital
Forensics and Cyber Security courses at the Institute of Technology Blanchardstown, Dublin.
1 Overview
The learning objective of this lab is for students to get familiar with the concepts of creating and checking
basic file hashes on your own system. After finishing the lab, students will gain first-hand experience on
creating and verifying file hashes. Moreover, students will also learn how to properly save passwords and
investigate how hackers typically attack databases of badly hashed passwords.
2 Lab Environment
I am assuming most students are on a windows based machine so we’ll look at options for window’s based
machines first but we’ll look at options for other OS’s in a later lab.
3 Lab Tasks
3.1 Task 1: Investigating Basic Hashing
To start this task, you should open your favorite text editor and create a file (hashme.txt) with the numbers 1
to 5 (one per line), as shown.
File: hashme.txt
1
2
3
4
5
Once you have created your file you should search for some on-line tools to help you calculate the MD5
and SHA1 hash of the hashme.txt file.
1. What is the MD5 of the hashme.txt file?
2. What is the SHA1 of the file?
3. Are the MD5 and SHA1 hashes the same length? Explain why you think this is the case?
4. Do you think your hashes match your classmates hashes? Why?
5. Open your hashme.txt file and add a space after one of the numbers. Recalculate both the MD5 and
SHA1 hashes. Have they changed much if at all from the original hashes we calculated?
6. If you changed the file name to hashme1.txt and recalculate the hashes, do you think the hashes will
change? Test and see what actually happens.
Secure Communications and Cryptography – Mark Cummins – ITB 2
3.2 Task 2: Setting up Some Tools
Obviously using on-line tools to calculate our hashes relies on us having on-line access and is a bit painful
so lets look at setting up some tools so we can perform the same tasks locally on our machines.
Using certUtil: From the window’s command line we can use the pre-installed Windows utility certUtil
that can be used to generate hash checksums:
certUtil -hashfile pathToFileToCheck [HashAlgorithm]
HashAlgorithm choices: MD2 MD4 MD5 SHA1 SHA256 SHA384 SHA512
So for example, the following generates an MD5 checksum of our file
CertUtil -hashfile C:\TEMP\hashme.txt MD5
GUI Tools: If your prefer a simpler GUI based option there are hundreds of tools that you can download
that will add a nice context menu option to calculate the hash of a file for you.
Registry Tweak: Windows does have one such tool built in, but it is disabled by default but you can enable
it using a registry tweak.
PowerShell: It’s also possible to write a small Powershell script to do the same task.
So you see we have lots of options when it comes to calculating file hashes locally.
Try These Exercises Before Moving On
1. Use thecertUtil utility to verify the hashes you calculated earlier.
2. Do a quick Internet search for some hashing tools that you can add to your own system and again use
them to verify the hashes you calculated in the previous steps.
3. Use the registry file included in the labs section on Moodle to enable the Window’s built in utility and
again use to verify the previous hashes.
4. Try to run the powershell script included in the labs section on Moodle.
5. Sometimes you might just want to calculate the hash of a string, such as a password. Which of the
tools that we’ve looked at will allow you to get the hash of a text string directly?
6. What is the hash of the text string ’password’?
3.3 Task 3: Investigating Hash Collisions
It has been shown that MD5 is not collision resistant; as such, MD5 is not suitable for applications like SSL
certificates or digital signatures that rely on this property.
Secure Communications and Cryptography – Mark Cummins – ITB 3
Try These Exercises Before Moving On
1. Read the original two papers which outlined how to attack MD5, available under the labs section on
Moodle.
2. Get a copy of the two hello.exe files on Moodle. Use any of the MD5 hashing tools that you
downloaded earlier to confirm that they are the same program. (i.e. Their hashes match). Now run
both programs.
3. Download the two shattered pdf files (again from Moodle) and again verify that their SHA1 hashes
are the same before opening and examining the files.
4. What do you think are the possible consequences of the two previous little tests on electronic contracts,
e-commerce and digital forensic in the legal system?
5. Check out the http://shattered.io/ website and details of the attack.
6. As a forensic examiner how would you go about verifying the integrity of your assets for a legal case?
7. For the two previous test cases get a different hash (SHA1 etc.) of the files. Do they match now?
3.4 Task 4: Making a Hash of Password Security
When we store any user’s information in a central location we are offering any would be attackers a large
target to try and attack. Why spend time trying to guess a single user’s password details etc. when we could
try get the password file/database and get them all for about the same work.
There have been some very high profile leaks/hacks/robberies in recent years of large databases of user
information. Some of these robberies have highlighted the need for those in charge of our data to protect
it. Hashes are one way functions so even given the hashes it should be impossible to get back the
original password.
Try These Exercises Before Moving On
1. Why should we never store password as plain-text?
2. Have you ever used a password reset function that was able to tell you your original password? What
does this mean about how they are storing passwords?
3. Outline briefly how an attacker who gets hold of the new hashed password file cannot guess the users
original password.
4. Given the hash of a password shown below can you tell which hashing algorithm was likely used to
hash them? How can you tell?
d177b4d1d9e6b6fa86521e4b3d00b029
5. Can you figure out what password string the previous hash represents?
Secure Communications and Cryptography – Mark Cummins – ITB 4
3.5 Task 5: Rainbow Tables
Great we’ve secured our new system, hashed all the passwords, our system is secure. Some hacker gets our
list of user names and hashes but we can be confident that or site is still secure. Or can we?
Try These Exercises Before Moving On
1. Do a quick search on the terms Rainbow Tables What are they? How do they work?
2. Check out these online tools.
https://crackstation.net/
https://hashkiller.co.uk/
http://crackhash.com/
What services are they offering? How are they doing it?
3. Create the hash of one of your own commonly used passwords (or a made up one) and put the hash
back into one of these on-line tools to see if it would have found your password?
4. Try googling my password hash from earlier to try cracking it. How do Google and other search
engines know these hashes?
5. Check out this actual Exxon Mobil Corporation database dump by the hacking group Anonymous in
Jun 2012.
http://pastebin.com/1ca3BR19
6. Are the passwords from the dump hashed? If so, which hashing algorithm was used? How can you
tell?
7. Try crack a few random passwords from this actual database dump.
3.6 Task 6: Salted Hashes
Rainbow tables mean that normal hashed passwords are no longer secure (they haven’t been for a long time)
and we shouldn’t just be storing hashed passwords in our databases. The trick is to use a salt. Basically
an impurity that we add to the password before we hash it which renders the rainbow tables useless.
1. To create a salted hash we concatenate some string (the salt) to either the beginning or the end of the
password. Get the MD5 hash of the password ’qwerty’ using the salt ’www.itb.ie’
2. Try googling the salted hash you just created to see if it can be found.
3. Do you think it would be better for a large website to use the same salt for all passwords or a different
salt per password? Why?
4. Do we need to save the salt and the hash in our database or just the hash?
5. If we save the salt and hash in our database doesn’t this allow the hacker to simply break the hash
again?
Secure Communications and Cryptography – Mark Cummins – ITB 5
4 Submission
For this Lab you DO NOT need to submit a lab report describing what you have done or what you have
observed. However you should ensure you completely understand all tasks asked of you. If you do have
any questions please don’t hesitate to ask. The goal of this lab is for you to understand all of the concepts
discussed.
