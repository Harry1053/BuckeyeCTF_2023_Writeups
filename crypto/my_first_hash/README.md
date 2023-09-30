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

