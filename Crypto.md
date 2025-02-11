# Algorithms
There are some common algorithms in CTF crypto challenges. 

## RSA
If given n,c, and e, use factordb (http://factordb.com/) and the below code (from John Hammond, found here: https://pastebin.com/ERAMhJ1v) to find c. 
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# @Author: john
# @Date:   2016-08-25 14:33:10
# @Last Modified by:   john
# @Last Modified time: 2016-12-03 11:16:39
 
from Crypto.Util.number import getPrime, inverse
import binascii
 
'''
This Python code tries to illustrate how RSA is done at a basic level.
'''
 
 
# At RSA's core, there are two PRIME factors, p and q.
# With this code, I just generate two large random prime numbers.
# p and q are typically NOT given to you in an RSA challenge.
bits_size = 256
#p = getPrime( bits_size )
#q = getPrime( bits_size )

 
 
# These two prime factors multiply to create n, which is "the modulus".
# n is typically GIVEN to you in an RSA challenge.
#n = p * q
 
 
# The plaintext is typically referred to as m. Since we are working
# with numbers and math, we treat the string information as hex.
# Obviously this is NEVER given to you in an RSA challenge.
#m = "This is the clear text message."
#m = binascii.hexlify(m)
#m = int(m, 16)
 
 
# Another value, called e, is "the exponent".
# Both e and n make up "the public key", which is meant to be common
# knowledge. This is why typically n and e are BOTH GIVEN in an RSA challenge.
# Typcially, e is 65537, which is 0x10001 in hex
e = 0x10001
 
 
# The ciphertext, c, is created by this ENCRYPTION formula here.
#    c = ( m ^ e ) % n
# See how e is the exponent and n is the modulus?
# That is how the ENCRYPTION takes place.
# Typically you are given the c in an RSA challenge and it is your task
# to DECRYPT it to the m value, the plaintext.
#c = pow( m, e, n )
 
 
# Now how do we decrypt? We need "the private key"....
# We call this d in RSA. Thanks to some handy mathematical functions,
# you can find "Euler's Totient", or "the Phi function" of a number.
# This is 'the number of numbers that are less than a certain number and share
# a common denominator with that certain number'.
# I know that is hard to wrap your mind around here, but thankfully it is MUCH
# easier for a prime number. For a prime number, it is simply that number minus 1!
 
# So, if you are given n, what you need to do is find the factors of n.
# Like we've seen, this is typically p and q. So, can we find the phi function
# of n? Well, n is prime, and so are its factors, p and q, so phi should just be:
p=269967471399519356371128763174813106357
q=287545525236502653835798598413374134819
phi = ( q - 1 ) * ( p - 1 )
 
c=62899945974090753231979111677615029855602721049941681356856158761811378918268
n = 77627938360345301510724699969247652387657633828943576274039402978346703944383
# Now, we can kind of unravel that modular arithmetic that was done during the
# ENCRYPTION formula. We can find the private key, d, with the MODULAR INVERSE,
# of e and phi.  
# I use a module to do this that is reworked to use Trey's function
#     https://github.com/JohnHammond/primefac_fork
d = inverse( e, phi )
 
# Now, we can do a similar thing like before, but this time for DECRYPTION.
#        m = ( c ^ d ) % n
# This time we raise to our private key as an exponent, but still take the modulus.
# And we have successfully decrypted RSA!
m = pow( c, d, n )

print repr(binascii.unhexlify(hex(m)[2:-1]))
```

Another option would be to use [dcode](https://www.dcode.fr/rsa-cipher). 

# Cipher
There are tons of ciphers out there that are used for CTF challenges. 

## Hexadecimal
Any cipher that has ```/x/x/x``` is most likely hexadecimal. 

## BCrypt
Any cipher that begins with "$2y$" is Brcrypt. 

## COW Programming Language
If the cipher text provided looks like ```MoO mOo moo mOo mOo MMM moO moO MMM MOO MOo moO MoO mOo moo mOo mOo mOo MMM moO moO moO
MMM MOO MOo moO MoO mOo moo moO MoO MoO MoO MoO MoO MoO MoO MoO MoO MoO MoO MoO MoO Moo```, it is probably [COW](https://esolangs.org/wiki/COW) programming lanuage. Use [CacheSleuth](https://www.cachesleuth.com/cow.html) to decode. 

## Rails
If the challenge references a "train" or "rails," then the cipher is most likely the Rail Fence cipher. The best option to decode is using cyberchef. 

## Single Byte XOR
Decrypt a single byte XOR using the following python script: 
```
#! /bin/env/python3

def single_char_xor(input_bytes,char_value):
	output_bytes=b'' #output bytes 
	for byte in input_bytes: #loop through each byte in input bytes
		output_bytes += bytes([byte ^ char_value]) # XOR each byte of input bytes with the selected byte
	return output_bytes, char_value
	

b=bytes.fromhex("4b424048574b46534f424d4657") #input hex here

for i in range (256): #loop through all possible bytes 
	output,char=single_char_xor(b,i) #push the char to xor 
	print("Output: " + str(output) + " Char: " + str(char))
```

## Brainfuck
If the cipher looks like: 
```
<+++++++>---------.------+++<><>+++----
```
It is definitely Brainfuck and can be decrypted using: https://www.dcode.fr/brainfuck-language

## Malbolge
If the cipher looks like: 
```
%${cy?}|{zs[q7utVrkji/mfN+Lbgfe^]#aC_X|Z<RW
```
It is definitely Malbolge and can be decrypted using: https://malbolge.doleczek.pl/

## Polybius
If the cipher looks like: 
```
413532551224514444425111431524443435454523114523114314
```
It is definitely a Polybius cipher and can be decrypted using: https://www.dcode.fr/polybius-cipher

## ROT13
It is also called the Caesar Cipher where the letters are shifted 13 spots from their original location. Use CyberChef to determine flag. 

## Wingdings
If the code looks like:  ♐●♋♑❀♏📁🖮🖲📂♍♏⌛🖰♐🖮📂🖰📂🖰🖰♍📁🗏🖮🖰♌📂♍📁♋🗏♌♎♍🖲♏ or it references "wings", then it is windings! Use an [online decryption tool](https://www.dcode.fr/wingdings-font )

## G-Codes
G-Codes often show up like: 
```
G1X126.4138Y0.0000
G1X126.9655Y0.2759
G1X127.2414Y0.8276
G0Z0.1
G0X125.3103Y5.7931
```

They can be analyzed using [ncviewer](https://ncviewer.com/). 

# Hashes
Hashes come in a variety of versions and have been presented a variety of ways on a CTF. 

## Hash Type
Determine the type of hash that is presented 
```hashid - Identify the different types of hashes used to encrypt data```
```hashid [-h] [-e] [-m] [-j] [-o FILE] [--version] INPUT```

## MD5
Find the MD5 hash of a given image 
```md5sum - compute and check MD5 message digest```

## SHA1
Find the SHA1 sum of a given file 
```sha1sum - compute and check SHA1 message digest```

## SHA256
Find the SHA256 hash of a given file 
```sha256sum - compute and check SHA256 message digest```

## Hashcat
Hashcat is a great resource for cracking hashes. With a high powered machine it becomes better and better at its job. Website: https://hashcat.net/hashcat/

# Certificates

## Certificate Signing Requests
Sometimes, there are challenges that require analysis of a CSR file. Use [CSR Decoder](https://www.sslshopper.com/csr-decoder.html) or openssl to analyze. 
```openssl req -in mycsr.csr -noout -text```

# NTLMv2

## Hash Recovery in Wireshark
Can pull hashes from wireshark for cracking with [NTLMRawUnhide](https://github.com/mlgualtieri/NTLMRawUnHide). 