# Web

## Authentication
Inspecting the authentication mechanism or means by which a user passes their username:password combination to the remote service can reveal information about flag location, admin credentials, or password guessing oppurtunities. 

### Admin Credentials in JS
Use developer tools in the browser to inspect the authentication procedure. Files can pop up on the network connection that point to how the user is authenticated. 

### Java Web Tokens (JWT) 
JWTs are a common way for sites to authenticate users. Burpsuite can be used to check for the JWT within the authentication bearer section of the request. Hashcat as as module (16500) to crack the JWTs. Cheat sheet for cracking and abusing JWT can be found [here](https://book.hacktricks.xyz/generic-methodologies-and-resources/brute-force#jwt). 

## File Upload 
If the CTF challenge needs you to drop a shell to get the flag or gain access to a system. 

### Upload Directories
When trying to find locations to drop a shell, look for directories that can be accessed remotely like /uploads /images /media /resources. 

### File extension filtering 
Webs servers sometimes only allow a certain list of uploaded files, if the extension is not allowed, it will not allow upload. To bypass, some extension filters split the name based on “.” so adding something like .jpg.php will be allowed for a php reverse shell.

## Fuzzing
Some CTFs dont allow much fuzzing, but in case they do. 

### Gobuster 
Gobuster is a tool that helps discover directories on a webserver via fuzzing. 
```
gobuster dir -u http://example.com -w wordlist.txt -x php,txt,html
```
### Wfuzz
Wfuzz is a tool to fuzz usernames and passwords. It can also be used to fuzz directories. 
```
wfuzz -c -z file,mywordlist.txt -d “username=FUZZ&password=FUZZ” -u http://shibes.thm/login.php
wfuzz -c -z file,big.txt http://shibes.xyz/api.php?breed=FUZZ
wfuzz -c -z file,wordlist -u "http://10.10.225.218/api/site-log.php?date=FUZZ" --hc "404" --hh=0
```
## Improper File Access
Webpages can fail to check access of a user, leaving them open to improper file access. 

### Path Traversal 
Check path traversal vulnerability using ```../../../../``` to back out of the current directory and view files in other directories. 

### Net Traffic
Common web-based network traffic-like CTF challenges are included below. 

### Cookies 
Most web pages have cookies. Sometimes the cookies themselves contain the flag or manipulating the cookies allows you to access the flag. The best option to change the cookie is using ```curl --cookie= "[cookie]=value"```. 

### User-Agent 
Changing the header data in a web request (like the User-Agent) can allow access to the flag or allow further access. The best option to do so is to use ```curl -H```. 

### Post Request Data
Some challenges require adding data to the header of a POST request. The best option to do so is using ```curl -d [data] url```. 

## Source Code
Inspecting the source code of the website can reveal hints to flags, directions to flags, or the flags themselves.

### Comments 
The comments within webpage source code can reveal flags. Sometimes the comments are colored green. 

### Included Files 
Some webpages have included files within the source code. The included files can lead to more investigation and source code analysis. Or the included files can point to other means by which to get the flag. 

### Stored XSS
Certain malicious JS is submitted and later on stored directly on the site. Use of the ```<script></script>``` can execute code. There can also be interesting information in the ```<p></p>``` and ```<img></<img>``` sections. 

### Reflected XSS
Often carried out through HTTP request. 
```
<https://somewebsite.com/titlepage?id=> <script> evilcode() </script> 10.10.100.27/reflected?keyword=hello or 10.10.100.27/reflected?keyword=<script>alert(1)</script> 
```
## SQL 
SQL injection is common for web CTF challenges. 

### Blind SQLI
Blind SQLI occurs when an error is not displayed, so you can make an assumption about the backend database and its information. 

### UNION SQLI
Keep adding NULLs until an error occurs. 
```
' UNION SELECT NULL-- ' UNION SELECT NULL,NULL-- ' UNION SELECT NULL,NULL,NULL-- 
```

### SQLMap 
SQLMap is an open source pen testing tool that automates the detection and exploitation of SQLi. 
```
sqlmap --url http://tbfc.net/login.php
sqlmap --url http://tbfc.net/login.php --tables --columns
```
It also has the capability to be used with burpsuite. 
```
sqlmap -r filename
sqlmap -r sqli_save --tamper=space2comment --dbms=SQLite --dump-all -p search --level=5 --risk=3
```
## XML
XML has some interesting vulnerabilities that you can use if the webpage uses an XML parser. 

### XML External Entity 
XXE can allow you to run system commands if the webpage has an XML parser. Use this: https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing. 
Burpsuite can help with looking at possible XXE vulnerabilities. Good code to use for XXE is: ```<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>```. 

