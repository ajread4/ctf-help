# Time

## Epoch Time
Unix uses epoch time for some logs, convert with [EpochConverter](https://www.epochconverter.com/). 

## Webkit Time
Some web browsers dont use epoch time, they use Webkit. Best to convert with [WebKitConverter](https://www.epochconverter.com/webkit).

# Emails

## eml_analyzer
You can examine .emil files with [eml_analyzer](https://github.com/wahlflo/eml_analyzer). 

# Phishing
Some challenges require you to phish a fake user 

## NC
Netcat can send emails using ```nc -c [host] [port]```. A good guide is here: [Netcat and Email](https://szclsya.me/posts/net/send-email-with-netcat/). Example code:

```
nc -C challenge.ctf.games 32503
220 red-phish-blue-phish-be0042c22eaa2d04-8864dc68d-nt7jg Python SMTP 1.4.6
EHLO 127.0.0.1
250-red-phish-blue-phish-be0042c22eaa2d04-8864dc68d-nt7jg
250-SIZE 33554432
250-8BITMIME
250-SMTPUTF8
250 HELP
MAIL FROM:<read.austin@gmail.com>
250 OK
RCPT TO:<swilliams@pyrchdata.com>
250 OK
DATA
354 End data with <CR><LF>.<CR><LF>
FROM: [AJ Read] <read.austin@gmail.com>
To: <swilliams@pyrchdata.com>
Date: Wed, 2 Oct 2024 21:00:00 -0400        
Subject: Marketing Ideas

Test these data concepts out for marketing! 

```

# Scripting
Some challenges require a small form of scripting. 

## Base64 Multiples
If something requires you to base64 decode something multiple times, dont re-invent the wheel: [base64multipledecode](https://base64-multiple-decode.netlify.app/)

# Audio
Examining audio files in CTFs is not always the most fun. But, there are some interesting tools to use to listen to the audio itself or look at the spectrum. 

## Audacity
Audacity is a great utility for examining WAV files. 

## DTMF Tones
DTMF tones are interesting additions as audio files to CTFs. There is a DTMF identifier [here](https://unframework.github.io/dtmf-detect/#/). 

# Comand Line Utilities
There are some awesome command line utilities that can help with CTFs. 

## Cut

Search for a specific word within a file, cut based on a certain column, sort them so that they are alphabetical, and then make sure they are all unique, finally, count the number of lines
    ```Command: grep word_to_search file_location | cut -d " " -f column_to_choose | sort | uniq | wc -l```

Format the output of a file so that you are only adding up the number of uniq values within certain columns
    ```Command: cat file_location | cut -d "[" -f2 | cut -d "]" -f1 | sort | uniq | wc -l```

Add up the total number of values (in this instance KB) within a certain column of a file 
    ```Command: cat access.log | cut -d "-" -f4 | cut -d " " -f2 | sed 's/KB//g' | paste -s -d+ - | bc ```

## Less
You can run a command with: ```!command ``` while in ```less```. 

## Grep
```grep``` is a great command for basic searching. One of the key flags is the ```-r``` or recursive flag. 

## Shell Type
To find out what type of shell you are running in: ```Command: echo $0```

## Diff
If you need to compare two files for differences, use ```diff [file1] [file2]```. There is also a way to compare recursively with ```-r```. 

## Diffuse
If you need to compare more than two files for differences, use ```diffuse [file1] [file2] [file3] [file4]```. 

# FileShare
Some challenges require you to interact with a network file share. 

## Smbclient
Used to access Samba share 
```
Command: smbclient //REPLACE_INSTANCE_IP_ADDRESS/**sharename**
```
# Geo
Geo challenges can deal with geolocations to find the flag based on coordinates, reverse image searches, etc. 

## Python GeoIP
Python has a geoip database (called geolite2) that can be used to find specific locations 
    the python script will look like: 
```
import geoip2.database
reader = geoip2.database.Reader('./GeoLite2-City_20200331/GeoLite2-City.mmdb')
```

## Reverse Image Search
Use the Google Reverse Image search tool to complete challenges that require you to find a location! 

# Password Cracking
There are great tools to use for cracking a password to grab the flag. 

## Fcrack
Crack a password using frcrack on a zip file with a wordlist. 
Some of the good options are: 
	-D option uses dictionary mode to read passwords from file with one password per line 
	-v option uses verbose mode, the more v's the more verbose 
	-u option uses unzip, tries to decompress the file while calling unzip during the breaking 
	-p option sets the initial starting password for brute force password searching  
	
```Command: fcrackzip -v -u -D -p rockout .zip_file*```

## John the Ripper
Decrypting passwords with John the Ripper when ```/etc/passwd``` and ```/etc/shadow``` are given. Before cracking with John the Ripper, the passwd and shadow files need to be unshadowed. 

## PDFCrack
Crack pdfs that are encrypted using a password. 
```Command: pdfcrack -w location_or_rockyou location_of_pdf```

## Zip2John
If provided with a zip file, you can try to crack the password to the zip file using john. But, you must first format using ```zip2john```. 

# QR Codes
Ever since COVID, QR codes have really been on the rise. 

## Zbarimg
Scan QR codes in a terminal. 
```zbarimg - scan and decode bar codes from image file(s)```

# Wifi
Wifi challenges are often used for OSINT, RF, or basic network information challenges. 

## Wigle
Wigle is a great wifi utility that basically shows networks based on location. There have been some challenges that required fetching the SSID or network name based on a certain geographic location. The website: ```http://wigle.net```

# Random Files
There are various random file formats that have been seen on CTFs. 

## DAE Files
DAE files can be inspected using a tool called blender which can be downloaded on Linux. Often DAE files are mechanical drawings for engineering. 

# Privilege Escalation
Sometimes challenges require you to escalate privileges and read a flag as root. 

## Compgen
compgen is a command line tool native to linux that can be run to determine what can be run in the terminal. Often, CTFs will drop into a low privilege or weird terminal that you need to get out of. 

## Python
In order to escalate privileges, it may be required to use python to do so. If so, the user can look at which libraries are called and in what order with ```python3 -c 'import sys; print("\n".join(sys.path))'```. 

# Command Line Tools with Bad/Tricky Terminal
Some CTFs drop a user into a bad terminal that requires little tricks to access the desired information. 

## Echo
Using ```echo *``` will read the contents of a directory if unable to use ```ls -la```. 

## SSH Access and Echo
There are challenges where ssh requires you to run commands immediately through using ```echo``` with ```echo "cat flag.txt" | ssh -p 30456 user@challenge[.]ctf[.]games```

# Git
There are some challenges that revolve around git repos like commits and pull history. 

## Log
Review the old commits from a git repo using ```git log -p -2```. 

## Branch
Look for specific flags within other branches with ```git branch```. 

# Python
There are some challenges that are specific for python code. 

## Symlinks
There is a possibility to read a file in python with ```f.read()``` where you can create a symlink to read another file. 

# PowerShell

## Download String
Sometimes Cobalt Strike payloads must be grabbed by the target using PowerShell. Best avenue is to google deobfuscation of PowerShell with Cobalt Strike Beacons. Example [here](https://medium.com/@polygonben/deobfuscating-a-powershell-cobalt-strike-beacon-loader-c650df862c34)

# Redis
Redis is a type of server that has been seen in previous CTFs.  

## Redis CLI
Use ```redis-cli``` to interact with the redis server to find the flags. 