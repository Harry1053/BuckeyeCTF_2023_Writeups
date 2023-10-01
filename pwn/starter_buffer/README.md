# Starter Buffer
### Category: PWN
### Difficulty: Beginner
### Author: geekgeckoalex

# Description

Tell me your favorite number and I might give you the flag ;).

# Attachments

nc credentials, buffer, Dockerfile, starter-buffer.c

# Solution

Although I could not immintly excecute a buffer overflow as I am used to (buffer size + 8 extra chars + function adress)

If you look at the attached start-buffer.c file, you will see that the address is given (0x45454545).
We want to go over the buffer size we are allowed to and overwrite the variable next to it, which is the flag variable. 
Example:
	Enter your favorite number: AAA
	Too bad! The flag is 0xaabdcdee

Since we know the targeted value, we can modify our input and get it to work. When we see that part of the flag is correct like here:

	Enter your favorite number: EEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE
	Too bad! The flag is 0xa454545

We can see that we are not overwriting just enough, so if we add one more E we should be getting the flag, which we are.


# Flag

bctf{wHy_WriTe_OveR_mY_V@lUeS}
