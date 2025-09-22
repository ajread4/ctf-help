# Forensics

## File Carving
Use ```dd``` to complete file carving using an example command like: ```dd if=Challenge1_Manual_Carve_usb.img of=Image.png bs=1 skip=134483968 count=463```. You can also use automatic tools like [Foremost](https://www.hackingarticles.in/forensic-data-carving-using-foremost/) or [Scalpel](https://github.com/sleuthkit/scalpel). 

## SQL
CTFs can provide you sql databases to analyze during this category of challenge. 

### Sqlite3 Command Line
Linux can interact with sqlite2 databases using the command line with ```sqlite3```. 

## Splunk
CTFs can provide versions of splunk for you to investigate. 

### HEC Tokens
If, when accessing splunk, it requests an authorization header. You likely need to find the HEC token for the instance and change the header using ```curl```. 

## Packet Capture
Sometimes, challenges want you to look at packet capture output. 

### Keyboard
Keyboard strokes can be identified with ```URB_INTERRUPT IN``` over the USB protocol. Each stroke can map to specific keys using the HID table from the Leftover Capture Data, filtered with ```usb.transfer_type == 0x01```. A script for mapping: 

```
import sys,os

lcasekey={}
ucasekey={}

lcasekey[4]="a";           ucasekey[4]="A"
lcasekey[5]="b";           ucasekey[5]="B"
lcasekey[6]="c";           ucasekey[6]="C"
lcasekey[7]="d";           ucasekey[7]="D"
lcasekey[8]="e";           ucasekey[8]="E"
lcasekey[9]="f";           ucasekey[9]="F"
lcasekey[10]="g";          ucasekey[10]="G"
lcasekey[11]="h";          ucasekey[11]="H"
lcasekey[12]="i";          ucasekey[12]="I"
lcasekey[13]="j";          ucasekey[13]="J"
lcasekey[14]="k";          ucasekey[14]="K"
lcasekey[15]="l";          ucasekey[15]="L"
lcasekey[16]="m";          ucasekey[16]="M"
lcasekey[17]="n";          ucasekey[17]="N"
lcasekey[18]="o";          ucasekey[18]="O"
lcasekey[19]="p";          ucasekey[19]="P"
lcasekey[20]="q";          ucasekey[20]="Q"
lcasekey[21]="r";          ucasekey[21]="R"
lcasekey[22]="s";          ucasekey[22]="S"
lcasekey[23]="t";          ucasekey[23]="T"
lcasekey[24]="u";          ucasekey[24]="U"
lcasekey[25]="v";          ucasekey[25]="V"
lcasekey[26]="w";          ucasekey[26]="W"
lcasekey[27]="x";          ucasekey[27]="X"
lcasekey[28]="y";          ucasekey[28]="Y"
lcasekey[29]="z";          ucasekey[29]="Z"
lcasekey[30]="1";          ucasekey[30]="!"
lcasekey[31]="2";          ucasekey[31]="@"
lcasekey[32]="3";          ucasekey[32]="#"
lcasekey[33]="4";          ucasekey[33]="$"
lcasekey[34]="5";          ucasekey[34]="%"
lcasekey[35]="6";          ucasekey[35]="^"
lcasekey[36]="7";          ucasekey[36]="&"
lcasekey[37]="8";          ucasekey[37]="*"
lcasekey[38]="9";          ucasekey[38]="("
lcasekey[39]="0";          ucasekey[39]=")"
lcasekey[40]="Enter";      ucasekey[40]="Enter"
lcasekey[41]="esc";        ucasekey[41]="esc"
lcasekey[42]="del";        ucasekey[42]="del"
lcasekey[43]="tab";        ucasekey[43]="tab"
lcasekey[44]="space";      ucasekey[44]="space"
lcasekey[45]="-";          ucasekey[45]="_"
lcasekey[46]="=";          ucasekey[46]="+"
lcasekey[47]="[";          ucasekey[47]="{"
lcasekey[48]="]";          ucasekey[48]="}"
lcasekey[49]="\\";         ucasekey[49]="|"
lcasekey[50]=" ";          ucasekey[50]=" "
lcasekey[51]=";";          ucasekey[51]=":"
lcasekey[52]="'";          ucasekey[52]="\""
lcasekey[53]="`";          ucasekey[53]="~"
lcasekey[54]=",";          ucasekey[54]="<"
lcasekey[55]=".";          ucasekey[55]=">"
lcasekey[56]="/";          ucasekey[56]="?"
lcasekey[57]="CapsLock";   ucasekey[57]="CapsLock"
lcasekey[79]="RightArrow"; ucasekey[79]="RightArrow"
lcasekey[80]="LeftArrow";  ucasekey[80]="LeftArrow"
lcasekey[84]="/";          ucasekey[84]="/"
lcasekey[85]="*";          ucasekey[85]="*"
lcasekey[86]="-";          ucasekey[86]="-"
lcasekey[87]="+";          ucasekey[87]="+"
lcasekey[88]="Enter";      ucasekey[88]="Enter"
lcasekey[89]="1";          ucasekey[89]="1"
lcasekey[90]="2";          ucasekey[90]="2"
lcasekey[91]="3";          ucasekey[91]="3"
lcasekey[92]="4";          ucasekey[92]="4"
lcasekey[93]="5";          ucasekey[93]="5"
lcasekey[94]="6";          ucasekey[94]="6"
lcasekey[95]="7";          ucasekey[95]="7"
lcasekey[96]="8";          ucasekey[96]="8"
lcasekey[97]="9";          ucasekey[97]="9"
lcasekey[98]="0";          ucasekey[98]="0"
lcasekey[99]=".";          ucasekey[99]="."

with open("/home/ajread/Downloads/out.txt",'r') as f:
    for line in f: 
        bytesArray=bytes.fromhex(line.strip())
        val=int(bytesArray[2])

        if val>3 and val<100:
            if bytesArray[0] == 0x02 or bytesArray[0] == 0x20:
                print(ucasekey[int(bytesArray[2])], end='')
            else: 
                print(lcasekey[int(bytesArray[2])], end='')
```

## Registry
NTUser.dat may be provided by the challenge. 

### reglookup
reglookup is a great command line tool for looking at registry data. 

### registryspy
Use [registryspy](https://github.com/andyjsmith/Registry-Spy) for a GUI version on linux. 

## Code
Code can be obfuscated from easy view. 

### Rubber Ducky
Some challenges provide rubber ducky code that can be obfuscated. use: https://ducktoolkit.com/decode# to decode the ducky code. 

### Code Beautifier
There is an awesome code beautifier, especially with PHP [here](https://codebeautify.org/php-beautifier#google_vignette)https://github.com/unode/firefox_decrypt
	
## File Specifications
There are some common ways to find out what type of artifact is provided during a challenge. 

### Magic Number
The magic number of a file is unique and shows what type of file something is. Use ```xxd``` or ```bless``` to exammine the file contents. 

https://www.geeksforgeeks.org/working-with-magic-numbers-in-linux/

Another resource is this: https://filesig.search.org/

### Create File
If provided just the contents of a hexdump, ```xxd``` has the ability to reverse the hexdump and recreate the file using the ```-r``` flag. 

### ISO Files
The best option to open up ISO/MP4 files is using VLC on Linux. The file is essentially an audio file. 

## Disk Image

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

### mmls
Gather information about the device img using ```mmls``` which can be useful to find the sector sizes and number of sectors. 

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
Network logs provided in forensics challenges can be in the form of Bro or Zeek logs. 

### Zeek-cut
Command zeek-cut works well to easily examine bro log columns and grep across them. It extracts the given columns from ASCII zeek logs on standard input, and outputs them to standard output. If no columns are given, all are selected. By default, zeek-cut does not include format header blocks in the output. 
```zeek-cut [options] [columns]```

### Rita
[Rita](https://github.com/activecm/rita/tree/master) can help identify beaconing activity from within Zeek logs. 

## Email
Some challenges require analysis of emails. 

### Email Headers
There are various tools to use for examining email headers to include [Message Header Analyzer](https://mha.azurewebsites.net/), [Google Message Header](https://toolbox.googleapps.com/apps/messageheader/analyzeheader), [Mail Header Analysis](https://mailheader.org/). There is also a good room on TryHackMe for email header analysis [here](https://tryhackme.com/room/phishingemails3tryoe). 

### Eml-extractor
You can extract the attachments within email files (.eml) for analysis using ```eml-extractor```.

## Web
There are some challenges that are forensics based with web adjacency. 

### Firefox Passwords
Passwords from firefox can be snagged from a ```login.json``` file. There is a good write up [here](https://medium.com/geekculture/how-to-hack-firefox-passwords-with-python-a394abf18016). The code can be found in Python on Github [here](https://github.com/unode/firefox_decrypt). 

## Image Analysis
There are some challenges that require you to analyze forensic images. 

### Binwalk
The command ```biwalk``` can be used to search in the slack space of a file. 

### Wimapply
[Wimapply](https://wimlib.net/man1/wimapply.html) is a great tool to view and interact with images that are described as "Windows imaging (WIM) image v1.13, XPRESS compressed, reparse point fixup."

### Volatility
[Volatility](https://github.com/volatilityfoundation/volatility) is the main forensics tool with any Windows image. It has a suite of capabilities to analyze many versions of the OS for data. 

### Strings
When it comes down to it, can always run ```strings``` against a memory image! 

### UHARC
If a file returns as UHARC, they can be analyzed via GUI or CMD (on a windows system) with [UHARC GUI](https://www.softpedia.com/get/Compression-tools/UHARC-GUI.shtml). Unix systems struggle to analyze these. Instead, shift over to a Windows system and view it. 
