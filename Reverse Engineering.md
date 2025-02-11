# Reverse Engineering

## Dynamic Analysis
Analysis of binaries and files can be done while running them! 

### EDB Bugger
[edb-bugger](https://github.com/eteran/edb-debugger) is a great tool for debugging. It is also available via the command line on some distros! 

## Binaries
Reverse engineering challenges often have to do with examining binaries and re-creating the flag for yourself. 

### Binwalk
A command to look through a binary. 
```
binwalk -e firmware.bin
```
### Ghidra
Use [ghidra](https://ghidra-sre.org/) to reverse engineer all binaries. 

### UPX
Some binaries are packed, you can use [UPX](https://github.com/upx/upx) to unpack binaries. 

### Go Binaries
If the binaries are written in Go, you can use [pygore](https://github.com/goretk/pygore) or [goretk](https://github.com/goretk). 

## Static Analysis
Analysis of executables or binaries can be done statically. 

### Ghidra
Use [ghidra](https://ghidra-sre.org/) to reverse engineer all binaries. 

### XXD
The xxd command returns a hexdump of the executable. 

### Objdump
Objdump is a command to display object data of a file. 

### Detect It Easy
Use [Detect It Easy](https://github.com/horsicq/Detect-It-Easy) to determine if something is packed and it's entry point. 

### CFF Explorer
Use [CFF Explorer](https://ntcore.com/explorer-suite/) to look at executable, similar to Detect It Easy. 

### UPX
Some binaries are packed, you can use [UPX](https://github.com/upx/upx) to unpack binaries. 

### Cobalt Strike Beacons
[1768](https://github.com/DidierStevens/DidierStevensSuite/blob/master/1768.py) is a great tool to analyze CS beacons that require investigation. 

## Java
Some challenges in CTFs require analysis of Java code. 

### Disassemble
Analyze java code using ```javap -c file.class``` on the command line. 

## Code
Some reverse engineering challenges require you to review code and see what it does. 

### Code Beautifier
There is an awesome code beautifier, especially with PHP [here](https://codebeautify.org/php-beautifier#google_vignette)https://github.com/unode/firefox_decrypt

### VBScript Encryption/Decryption
If there is any mention of WScript or VBScript, use the decryption tool [here](https://master.ayra.ch/vbs/vbs.aspx). 