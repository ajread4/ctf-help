# Forensics

## Code 
Code can be obfuscated from easy view. 

### Rubber Ducky
Some challenges provide rubber ducky code that can be obfuscated. use: https://ducktoolkit.com/decode# to decode the ducky code. 

## File Specifications 
There are some common ways to find out what type of artifact is provided during a challenge. 

### Magic Number
The magic number of a file is unique and shows what type of file something is. Use ```xxd``` or ```bless``` to exammine the file contents. 

https://www.geeksforgeeks.org/working-with-magic-numbers-in-linux/

### Create File 
If provided just the contents of a hexdump, ```xxd``` has the ability to reverse the hexdump and recreate the file using the ```-r``` flag. 

## Floppy Disk
### QEMU
QEMU is a great resource for examing a floppy image. Example command: 
```
qemu-system-i386 floppy.img
```

boot a floppy image with qemu-system-i386, make sure that the image has file output: DOS/MBR boot sector
    qemu-doc - QEMU version 4.0.0 User Documentation
    qemu-system-i386 [options] [disk_image]
    

open up qemu-system-i386 in pause mode so that you can stop
    ```qemu-system-i386 -monitor stdio -S ```
    start up a gdbserver within the monitor with: ```gdbserver```
    connect to the gdbserver for qemu on a seperate terminal 
    set a watchpoint for EIP 
        needs to be done with, for example, ```*((char[64]*)(0x7dc0))```
    use ```continue``` to work through the gdb session to find the flag 

open up qemu monitor to inspect floppy image at a different location 
    command with -monitor will open monitor 
    within monitor: 
        ```xp /20c 0x7DC0``` will look at the specific location for value 
        use help menu within monitor

### Boot Sector 
For some floppy images, it is necessary to change portions of the image using ```bless```. Usually this occurs because running the ```file``` command on the image returns something unexepcted or incorrect. In one CTF, the last portion of the boot sector in a floppy image had to be ```0xAA55``` to be able to boot properly as MBR DOS. To make sure it is read properly, use the ```file``` command again and see if it reads as the corrected file type. 

## Wireshark 
Wireshark is a great forensics tool for looking at network data. There are tons of tips and tricks with the tool. 

### HTTP Requests 
Using wireshark to search for specific HTTP GET requests 
```Command: http.request.method == GET```

### URL Status Codes 
Searching for network traffic where the URL requested was not found, look for http status code 404. 

### HTTP Get Requests 
The HTTP Get request often contains information regarding the client like User-Agent. 

### Cache Information 
Cache-Control has interesting values like max-age that recommend how long a server recommends the connection be kept in tact. There have been a few challenges that I have had to change the values. 

### VNC
If the challenge requries you to find the workstation running NVC search pcap for VNC protocol. 

### Mail Server 
If the challenge requries you to find the workstation running mail server search pcap for SMTP protocol. 

## Zeek Bro
Network logs provided in forensics challenges can be in the form of Bro or zZeek logs. 

### Bro-cut
Command bro-cut works well to easily examine bro log columns and grep across them. It extracts the given columns from ASCII Bro logs on standard input, and outputs them to standard output. If no columns are given, all are selected. By default, bro-cut does not include format header blocks in the output. 
```bro-cut [options] [columns]```