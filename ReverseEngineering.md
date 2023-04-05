# Reverse Engineering 

## Binaries 
Reverse engineering challenges often have to do with examining binaries and re-creating the flag for yourself. 

### Binwalk
A command to look through a binary. 
```
binwalk -e firmware.bin
```
## Static Analysis
Analysis of executables or binaries can be done statically. 

### XXD
The xxd command returns a hexdump of the executable. 

### Objdump 
Objdump is a command to display object data of a file. 

## Java 
Some challenges in CTFs require analysis of Java code. 

### Disassemble
Analyze java code using ```javap -c file.class``` on the command line. 