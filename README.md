# blazectf
I only solved the two magic challenges during this competition.
## magic-re
This was a pretty straightforward challenge that you don't need to understand the binary to do. IDA decompiler threw a weird error but let me see the code after decompiling the scanf function, although the decompiled code was faulty. I noticed it waslooping through your input string and doing a magic function and strcatting the output to a string at 0x31338000, and after several loops of this it compared the value there to some static values at a buffer at 0x3133a000. I didn't even look at the magic function and just decided to bruteforce the flag char by char, as since it was looping through your input in order you could just compare the string at 0x31338000 to the first few chars at 0x3133a000, breaking in gdb every time it did a strcat. 

I used the script attached to kind of manually bruteforce the flag with gdb scripting-- the length of the output kept changing and I couldn't figure out why, so I just used x/700xw to print a bunch of values at each location, and compared the first few bytes of each output. This was annoying because some null bytes at the end were printed with 0x31338000 and I didn't know how much to truncate and didn't feel like parsing the output either, so I had to change the number of bytes I wanted to compare. One way to fix this is to write a parser for the x/xw output or just use x/xs. The flag is blaze{^_^ONE_BYTE_INSTRUCTION_FLAG_IZ_CLASSY_AND_FUN_B]}
## magic-pwn
It's pretty obvious we need to understand the magic function for this one :(. 
