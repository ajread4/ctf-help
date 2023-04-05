# Steganography

## Images 
Some CTF challenges require analysis of images for colors, space, hidden words, etc. 

### GIMP 
Gimp is an image manipulation and paint program. If you are given two images and it appears that you need to lay them on top of each other to find the flag use gimp and change the opacity. 

### pngcheck
pngcheck examines a pngfile for possible flags or other hidden information. Information about the tool can be found [here](https://wiki.bi0s.in/steganography/pngcheck/)

## Metadata
For many stegonagraphy challenges, the flags are hidden within the metadata. 

### stegoVeritas
The catch-all tool for stego that runs a combination of various tools below. It can be downloaded on github: https://github.com/bannsec/stegoVeritas. 

### Zsteg
Another stego tool that must be installed using ruby. 

### Exiftool 
Exiftool is a great command line tool for reading metadata from a file. 

### Strings 
Strings prints the printable characters within a file, no matter the file. This command is also helpful for forensics and reverse engineering challenges. 

### Identify
Identify is a command that prints characteristics of an image file. The verbose flag outputs important metadata for CTFs. 

### Stegsnow 
Stegsnow is a great command to find information in the whitespace of an image. 

### File 
The file command expresses the type of file provided. It examines the header data of a file and returns the file type. 

### Bless
Bless is a graphical editor of files and allows you to change the file itself like the magic number, header data, boot location, etc. 

## Office Products 
Some CTF challenges provide office products like excel, word, or powerpoint. Often, the office product contains a

### Olevba
Examine Microsoft office documents for macros using olevba, which is a script to parse OLE and OpenXML files such as MS Office documents and to extract VBA Macro code in clear text, deobfuscate and analyze malicious macros.

```Command: olevba location_of_file```

## Oledump		
Examine OLE files where it searches for streams of data within Office files that could hold malicious macros. 

### PDFs 
PDFs have some interesting stego challenges. 

### pdf-parser.py
A tool that can identify fundamental elements of PDFs
```
pdf-parser.py –filter –raw –object 237 ouch.pdf
pdf-parser.py –filter –raw –type /Filespec ouch.pdf 
pdf-parser.py ouch.pdf –filter –raw –object 235 -d ouch_embedded.txt
```

### pdfid.py
A tool to test a pdf file, looks for PDF keywords within PDF file. 

### peepdf.py
A tool to look at specific objects and object streams within possibly malicious PDFs

### pdfwalker.py
A tool that can allow you to walk through a PDF via a GUI, most likely use on Windows machine to inspect PDF. 