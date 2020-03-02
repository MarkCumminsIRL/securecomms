| Secure Communications – Mark Cummins – TUDublin | 
| ------ | 
|These notes and exercises are part of the Secure Communications module on the Digital Forensics and Cyber Security course at Technological University Dublin. |




## Lab 6A: Python Challenge - Simple Hash Chains

OK for this lab you need to use python code to solve a simple hash chain or blockchain problem.
___

### Lab Contents

1. Scenario
2. Procedure
3. What is a Hash Chain?
4. The Seed Value
5. The Solution
6. Submission
___

### 1. Scenario

You've registered for an online service that uses hash chains. You've registered as user 'nOOB’ and have been given the hash chain
seed 654e1c2ac6312d8c6441282f155c8ce9


Use the given information to figure out how to authenticate as the user 'ECSC' for the given challenge hash c89aa2ffb9edcc6604005196b5f0e0e4
i.e. Find the hash that hashes to this - This hash will be your solution.


### 2. Procedure:

1. First let's see how to calculate hashes in python.

You should be able to use the following bit of code to calculate the MD5 of the the string “Hello World!”

```python
# import the hashlib library for performing hashing functions
import hashlib

# Create an initial test string
some_string = "Hello World!"

# Create an MD5 hash object
hash = hashlib.md5()

# Update our hash object with the string
hash.update(some_string)

# Print out our hash in hex format
print (hash.hexdigest())
````

### 3. What is a Hash Chain?

Our next step is to understand what a hash chain is. So normally a hash chain is a hash value that we hash again, and again etc to produce a chain.  

So  
A = MD5(‘seed’)  
B = MD5(A)  
C = MD5(B)  
Etc.  

Or MD5(MD5(MD5(‘seed’))  

This produces a chain of hashes, and we keep going until the hash that we get is equal to the hash we are looking for (The challenge hash), so in our example we need to find ‘c89aa2ffb9edcc6604005196b5f0e0e4’


### 4. The Seed value

The final piece of the jigsaw is to understand the ‘seed’ value. The seed value is the initial starting point of the hash chain. It’s the original string that we hash and might normally be a user’s password or similar. 


For our example this last step has a bit of a trick in it.. I suggest googling the seed given for the user nOOB and try to figure out how the seed value for this user is generated. Once you figure this out you need to calculate the seed for the user ECSC and then work out the hash chain until you reach the challenge hash.


### 5. The solution 

The solution will be the hash that actually maps to the challenge hash, so the second last hash in our chain as such.  
Good luck.


### 6. Submission

You should submit the final hash and your final python code to solve the challenge. You'll be asked to show your code on github and demo and explain it working during the lab.
