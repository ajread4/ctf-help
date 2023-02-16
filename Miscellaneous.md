# Audio
Examining audio files in CTFs is not always the most fun. But, there are some interesting tools to use to listen to the audio itself or look at the spectrum. 

## Audacity
Audacity is a great utility for examining WAV files. 

# CMDLine 
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
To find out what type of shell you are running in:
    ```Command: echo $0```

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

# QR Codes
Ever since COVID, QR codes have really been on the rise. 

## Zbarimg
Scan QR codes in a terminal. 
```zbarimg - scan and decode bar codes from image file(s)```

# Wifi 
Wifi challenges are often used for OSINT, RF, or basic network information challenges. 

## Wigle
Wigle is a great wifi utility that basically shows networks based on location. There have been some challenges that required fetching the SSID or network name based on a certain geographic location. The website: ```http://wigle.net```


