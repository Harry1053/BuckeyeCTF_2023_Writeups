# Ruvest-Shamir-Adleman
### Category: Crypto
### Difficulty: Beginner
### Author: jm8

# Description

Big numbers make big security

# Attachments

dist.py

# Initial Thoughts

The first thing that I thought of after reading the title was RSA. The challenge name consists of the lastnames of the three founders of RSA.
The description also seemed to be supporting my idea, as in RSA the bigger the numbers, the safer it is.
These thoughts got confirmed when I looked at the python script.

	message = b"[REDACTED]"

	m = int.from_bytes(message, "big")

	p = 3782335750369249076873452958462875461053
	q = 9038904185905897571450655864282572131579
	e = 65537

	n = p * q
	et = (p - 1) * (q - 1)
	d = pow(e, -1, et)

	c = pow(m, e, n)

	print(f"e = {e}")
	print(f"n = {n}")
	print(f"c = {c}")


	# OUTPUT:
	# e = 65537
	# n = 34188170446514129546929337540073894418598952490293570690399076531159358605892687
	# c = 414434392594516328988574008345806048885100152020577370739169085961419826266692

# Solution

The combination of n, c, e p and q is very common in CTF RSA challenges as since the numbers are relatively small they are easy to crack.

Our steps are:

1. Calculate \(\phi(n) = (p-1)(q-1)\).
2. Find the modular multiplicative inverse of \(e\) modulo \(\phi(n)\). This is often done using the Extended Euclidean Algorithm.
3. The result from step 2 is your private exponent \(d\).
4. Decrypt the ciphertext \(c\) using \(m \equiv c^d \mod n\).



If we do that properly, we get successfully get the flag.

# Flag

bctf{1_u53d_y0ur_k3y_7h4nk5}
