# My First Hash
### Category: Crypto
### Difficulty: Beginner
### Author: geekgeckoalex

# Description

Here's your flag: 8f163b472e2164f66a5cd751098783f9 Psyc! Its encrypted.
You think I'd give it to you that easily? Definitely don't look at my code tho -><- (when you find the flag, put it in bctf{} format)

# Attachments
A python file named "my-first-hash.py".

# Initial Thoughts


The challenge seems straight forward, we are being given a hash.
We do not know what encryption it has, but we can find that out by looking at the python script.

	import hashlib
	from sys import exit

	flag = '8f163b472e2164f66a5cd751098783f9'

	str = input("Enter the flag\n")
	str = hashlib.md5(str.encode())

	if str.digest().hex() == flag:
		print("Congrats! You got the flag!")
	else:
	        print("Nope. Try again!")
	exit()

Here it is made obvious that the encryption is md5 as we can see in line 7.
After line 7 there is a simple set of if-else conditions so we can check whether the flag we got is correct.
We could write a script that runs this python code, and encodes one of many words to md5 and compares the hash to the flag-hash, to see whether that would be correct.
The approach I used though that is fairly faster is using hashcat.

# Solution

	$ hashcat "8f163b472e2164f66a5cd751098783f9" /usr/share/wordlists/rockyou.txt --force -m 0

Command breakdown:
First of all we write the first argument we supply is the hash that we got from the chall description and the python file.
After that, we enter the path to the wordlist we want to use, since this is a beginner marked challenge it is safe to assume the word will be present in rockyou.txt
We indicate "--force" because since we are working with an MD5 hash, this will make it ample faster. 
Last but not least we use "-m 0" to indicate that this is an MD5 hash.

Output (here it is cropped, due to its lenght):

The line we truly care about right now:
	
	8f163b472e2164f66a5cd751098783f9:orchestra

# Flag

bctf{orchestra}
