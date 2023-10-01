# 8ball
### Category: Reverse Enginerring
### Difficulty: Beginner
### Author: rene

# Description

Let me guide you to the flag.

# Attachments
8ball

# Solution

If we run the file we get prompted to ask the 8ball something, but nomatter what we input, we get the corresponding similar output:

	$ ./8ball a
	You asked:
	"a"
	Hmmm....
	Signs are not favorable.

If we open up the file in a decompiler like Ghidra, we can read through the main function and see the following:

	if ((local_c != 0) && (pcVar3 = strstr(param_2[1],"flag"), pcVar3 != (char *)0x0)) {
		puts("Why yes, here is your flag!");
		print_flag();
		return 0;

The important information here is that in order for the "print_flag" function to fire, we have some conditions. The first one is that the variable "local_c" is not set to 0. The other important one is that the first parameter is "flag".

We can browse the code again more careful to find this:

	local_c = 0;
	iVar1 = strcmp(*param_2,"./magic8ball");
	if (iVar1 == 0) {
		puts("Why, I guess you\'re right... I am magic :D");
		local_c = 1;


Here we see that the variable "local_c" is being initiallised and set equal to 0. Then the "strcmp" function is being called to check our input. It checks for the 0th parameter, the file name itself.
Thus, if we rename the file from "8ball" to "magic8ball", that should set local_c equal to 1, hence fullfilling the first condition.

For the second condition we merely have to type in flag as the second parameter to then get the flag.

	$ mv ./8ball ./magic8ball

	$ ./magic8ball flag

# Flag

bctf{Aw_$hucK$_Y0ur3_m@k1Ng_m3_bLu$h}
