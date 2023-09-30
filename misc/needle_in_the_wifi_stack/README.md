# Needle in the Wifi stack
### Category: Misc
### Difficulty: Easy
### Author: arcsolstice

# Attachments
frames.pcap.

# Initial thoughts
Since it is a packet capture file I opened it in wireshark but found nothing of interest, no major streams to follow.

# Solution
I extracted all strings from the file by using the strings command. I removed duplicates. I ended up with lots of what seemed to be base64 encoded strings.
Lots of them (see solve.py file). I saw that lots of them were very similar, with slight differences. I decoded some, and found that there were groups of strings with slight variations, like: "No Flag Here", "N0 Flag H3r3" and so on.

I was about to decode all of them by hand when luckily one of the strings decoded to "dont do it all manually" which gave me the idea to write a script for that (solve.py).
The script takes each item from a list, decodes it from base64 and prints it. I saw that there were lots of errors (from my error function). Those that were groubed together I did not care about, but there was one in the middle of proper prints, which made me look at it. I decoded it differently and got the flag. I think that if the python script were written more proficiently, the flag would have printed properly.

	b34c0n fr4m35, 5o hot ri6ht now
	b3acon fr4m35, s0 h07 ri6h7 now
	b3acon fr4m3s, 50 hot right now
	b3acon fram3s, 5o ho7 right n0w
	**Error decoding snippet: [...]**
	be4con fram3s, 50 h0t right n0w
	be4con frame5, s0 hot ri6ht now
	beacon fram35, 50 h0t ri6ht n0w

# Flag

bctf{tw0_po1nt_4_g33_c0ng3s7i0n}
