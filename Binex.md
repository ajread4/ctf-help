# Binary Exploitation

## C Code
C code has some interesting vulnerabilities when it comes to binary exploitation. 
### Max Value
Below has a good explanation with example code. I got this from the AllArmyCTF.
```
int tmp = first * second;
  /* In some languages (e.g. Python 3) there are no issues with the line above
   * and it will always match the intuitive meaning: `tmp` equals the product
   * of the two integers that were passed in and is therefore positive.
   *
   * However, this is not how C (or most languages with fixed-width integers)
   * works.  Instead the calculation can "overflow" the highest expressible
   * integer and wrap around to the lowest expressible integer and keep going.
   * In other words, it is entirely possible to get a negative number for
   * `tmp` by multiplying two numbers that are less than INT_MAX (2147483647).
   *
   * In the line below, we create the vulnerability by using `tmp` to access
   * the "numbers" array in our struct.  In C the modulo operator (%) (also
   * known as "remainder"), has the same sign as the left-hand side.  This
   * means if `tmp` is negative, we will end up accessing memory that is
   * outside of the array.
   *
   * How can we leverage this to print the flag?
   */
  printf("%d * %d = %d which ends in a '%s'\r\n",
         first, second, tmp, s.numbers[tmp % 10]);
}
```
### Format Specifiers
String format specifiers in C like ```printf``` and the use of ```%s``` allow you to execute commands. Can also use ```%x``` to print out the stack. If so, make sure to swap the endianess (to reverse what is displayed) and convert from hex using cyberchef. 


### Heap Manager Optimization (```tcache```)
There is a good explanation of heap manager optimization [here](https://github.com/Dvd848/CTFs/blob/master/2021_picoCTF/Cache_Me_Outside.md) in solving a PicoGym challenge. 

### Checksec
Use ```checksec``` to check executable properties post download. Command example is ```checksec --format=cli --file=vuln```. 

### Unlimited Length Input
In the C code, there can be times when the input string can be of unlimited length with ```__isoc99_scanf("%[^\n]",local_88);``` as an example but the buffer is limited in size with ```byte local_88 [112];```. This situation points directly to a buffer overflow/ROP attack vulnerability. 

### Position Independent Execution
If running ```checksec```, the binary can sometimes state "No PIE." If so, it means the binary runs from the same memory address each time. As a result, you can leak addresses from the stack to use! 

### Pwninit
Utilize [pwninit](https://github.com/io12/pwninit) for starting up challenges that provide binaries, libc, and makefiles. 

### Gdb
Use ```gdb``` on the command line to interact with compiled binaries. More information [here](https://sourceware.org/gdb/). 

### Use After Free Vuln
If there are sections of code with ```free()``` and specific variables, attempt a [Use after free](https://learn.snyk.io/lesson/use-after-free/use) to interact with the information. 

## ROP Exploitation

### puts
A ROP exploitation technique can rely on the ```puts``` function to display what is stored at the addressed passed in the argument. 

### pattern_create.rb
Use the tool ```pattern_create.rb``` in Metasploit to create a pattern that helps find RIP for you post segmentation fault. 

### pattern_offset.rb
Use the tool ```pattern_offset.rb``` in Metasploit to determine the offset of RIP when completing attack after segmentation fault operation. 

### ROPGadget
Use [ROPGadget](https://github.com/JonathanSalwan/ROPgadget) as a tool to facilitate exploitation! Explanation of the operation [here](https://ir0nstone.gitbook.io/notes/types/stack/return-oriented-programming/gadgets). 

### Gdb info frame
Use ```info frame``` in GDB to identify the pivotal information on the stack at fault. 

```
(gdb) info frame
Stack level 0, frame at 0x7fffffffdc20:
 rip = 0x400770 in do_stuff; saved rip = 0x3765413665413565
 called by frame at 0x7fffffffdc28
 Arglist at 0x4134654133654132, args: 
 Locals at 0x4134654133654132, Previous frame's sp is 0x7fffffffdc20
 Saved registers:
  rbp at 0x7fffffffdc10, rip at 0x7fffffffdc18

```

### Pwntools
Use [pwntools](https://docs.pwntools.com/en/latest/) to exploit binaries. It is a crazy capability with a ton of use cases. 

### Position Independent Execution
If running ```checksec```, the binary can sometimes state "No PIE." If so, it means the binary runs from the same memory address each time. As a result, you can leak addresses from the stack to use! 