# Cryptography

# 1) miniRSA-

the challenge which was extremelyyyy frustrating. RSA is encryption technique used over the internet and apparently is reallly hard to break thats why all our data transferred over internet is safe.

For the challenge, we are gievn with a text file with value of N and the cipher text.

![image](https://github.com/user-attachments/assets/094fd678-1281-4384-9a5c-f9405c718c21)

![image](https://github.com/user-attachments/assets/6cb6f477-75a9-4a2f-8a0c-f1f70a2fd229)

So firstly i needed to understand what RSA is-

https://en.wikipedia.org/wiki/RSA_(cryptosystem)

i followed the above link to somewhat understnad what it is, i couldnt understand anything so i had to watch some youtube videos.

1st link-https://www.youtube.com/watch?v=JD72Ry60eP4 \
2nd link-https://www.youtube.com/watch?v=-ShwJqAalOk

I watched these videos about whats RSA and how to break RSA.
I will try to explain how RSA works from my understanding.
- Two large prime numbers, p and q, are selected.
- The product of p and q (n=p⋅q) is calculated; n is used as the modulus.
- A public exponent e is chosen such that it is coprime with (p−1)(q−1).
- A private exponent d is computed, which is the modular multiplicative inverse of emod(p−1)(q−1).

Anyways to now think of what i have to. From the video I watched earlier tried python to solve this. However I got lost in the calculation.

I tried to think about someway to avoid this hectic calculations.so went through the wiki page again and saw the 2nd hint.

![image](https://github.com/user-attachments/assets/0d1a4a63-b0ee-4bdb-9959-ecd0bcd701bb)

So the main thing here is that m < n^(1/e). So basically I had to take the cube root of cipher text to easily get the message.So the first thing I did was to go to python and tried to cube root it using pow.

```
n=2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141

m= n**(1/3)
print(m)
```
however this script didnt give me the correct answer so tried another one which i found on stackoverflow.
```

def diff(n, mid):
    if (n > (mid * mid * mid)):
        return (n - (mid * mid * mid))
    else:
        return ((mid * mid * mid) - n)

# Returns cube root of a no n


def cubicRoot(n):

    # Set start and end for binary
    # search
    start = 0
    end = n

    # Set precision
    e = 0.0000001
    while (True):

        mid = (start + end) / 2
        error = diff(n, mid)

        # If error is less than e
        # then mid is our answer
        # so return mid
        if (error <= e):
            return mid

        # If mid*mid*mid is greater
        # than n set end = mid
        if ((mid * mid * mid) > n):
            end = mid

        # If mid*mid*mid is less
        # than n set start = mid
        else:
            start = mid


# Driver code
n = 205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141
print("Cubic root of", n, "is",
    round(cubicRoot(n), 6))
```
ahhh but this script tooook to long, ike i kept it running for like an hour and i still couldnt get the answer. At this point I wassss really lost.

So like any CTF i searched up RSA decoder and found dcode.fr website.

I put in the values and well i think i got the flag.
![image](https://github.com/user-attachments/assets/6f4017ed-8c5e-4ae6-a854-bd9e27bbf84e)

``` 
flag-picoCTF{n33d_a_lArg3r_e_d0cd6eae}
```
Voilaa

# 2) C3-

![image](https://github.com/user-attachments/assets/b5c66626-518c-422b-bbf2-ce2735281714)

so challenge begins with 2 files were given ciphertext and the encoder used to encode it which was a python file.

```
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
```
This was the python script used and the cipher text was DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl.

So firstly i tried to understand whats going on in the code, so it looks up the character from from lookup1 and finds its index then subtract the index from prev index of lookup1. 

so tried to make python script to decode it

```
chars = "DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl"


lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup2.index(char)
  ch= lookup1[(cur + prev) % 40]
  out+=ch
  prev = lookup1.index(ch)

print(out)
```

It took some time to understand what this is but after some trial and error i got.

so the output i got was 
```
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```

well it said self input so couldnt use a python editor to use this and also it was a python 2 program. But then i tried to make this program to have the same logic.

```
chars="""#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1"""

b=1
for i in range(len(chars)):
  if i==b**3:
    print (chars[i])
    b+=1
```
the output it gave was-
a
d
l
i
b
s
```
so flag is-picoCTF{adlibs}
```
# 3) Custom-Encryption-

all right for this challenge we were gievn with a python file and which is the encoder and a ciphertext.

![image](https://github.com/user-attachments/assets/c05603ce-fa2a-416b-8e2c-4a77f4c347f5)

the script given was-
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```
so I analysed the script and understood that there are two encrytion done on the flag.

- Firstly  a key is generated from two prime numbers which is then shared
- Then first encrytion is done in which the plain text is dynamically xored
- Then the cipher text is then stored as numerical value in list.

cipher text-[260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0, 2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921, 173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461, 347076, 491691]

soo i developed this python script to decode the flag-
```
def generator(g, x, p):
    return pow(g, x, p)


def decrypt(cipher, key):
    decrypted = []
    for num in cipher:
        try:
            decrypted_char = chr(num // (key * 311))
            decrypted.append(decrypted_char)
        except ValueError:
            print(f"Error decrypting {num}")
            decrypted.append('?')
    return ''.join(decrypted)


def dynamic_xor_encrypt(plaintext, text_key):
    
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    
    p = 97
    g = 31
    a = 94
    b = 29
    print(f"a = {a}, b = {b}")

 
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)

    
    if key != b_key:
        print("Invalid key. Aborting.")
        return

    shared_key = key
    print(f"Shared Key: {shared_key}")

   
    semi_decrypt = decrypt(plain_text, shared_key)
    print(f"Semi-Decrypted Text: {semi_decrypt}")

    
    completed_encryption = dynamic_xor_encrypt(semi_decrypt, text_key)
    print(f"Final Encrypted Text: {completed_encryption}")
    return completed_encryption



cipher = [
    260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0,
    2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921,
    173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461,
    347076, 491691
]
test_key = "trudeau"

# Run test
result = test(cipher, test_key)
flag=''
for i in result[::-1]:
    flag+=i
print(flag)
```
and the output from this code was-

```
a = 94, b = 29
Shared Key: 93
Semi-Decrypted Text:    VWDAE*SDV>3 1

Final Encrypted Text: }cd22a157_d6tp0rc2d_motsuc{FTCocip
picoCTF{custom_d2cr0pt6d_751a22dc}
```

so the flag is 
```
picoCTF{custom_d2cr0pt6d_751a22dc}
```
# 4)Vignere

All right so i already have some knowledge about Vignere cipher but i still searched up some research about it.

For the challenge we are given with the flag as a vignere cipher.

![image](https://github.com/user-attachments/assets/1b0f815c-8d29-46e0-a573-52b923fcc378)

So the cipher given was 
```
rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_cc82272b}

```
and key given is 
```
```
CYLAB
```

so well i usually use a tool called dcode.fr to decode ciphers so i saerched dcode and typed in the cipher with the key and got the flag 

```
picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_ae82272q}

# 5) HideToSee

For this challenge we are given with an image and hints says we have to extract it

![image](https://github.com/user-attachments/assets/3f4aefad-9fd3-4537-8155-db75c68b6896)

so i downloaded it and the image was like a the key to encryption however no text was given.

![atbash](https://github.com/user-attachments/assets/bb944997-9227-4256-a365-7f7a3fb612d8)

so the first thing i did was to use an online tool used to do all type of analysis of an image.
![image](https://github.com/user-attachments/assets/1d5c9090-d4e5-4c52-9ce6-3985003f4da7)

when i saw the steghide section i see a encryption.txt in it so i downloaded the zip file and extracted the txt file. and found a crypted flag.

```
krxlXGU{zgyzhs_xizxp_zx751vx6}
```

so to dicipher it  wrote a python code 

```
Cipher = "krxlXGU{zgyzhs_xizxp_zx751vx6}"
cipher1=Cipher.lower()
key="abcdefghijklmnopqrstuvwxyz"
decrypt=''
for i in cipher1:
    if i in key:
        ind=len(key)-1-key.index(i)
        decrypt+=key[ind]
    else:
        decrypt+=i
    
    
print(decrypt)

```
which gave me the flag as an output

```
picoctf{atbash_crack_ac751ec6}

```
# 6)ReadMyCert

![image](https://github.com/user-attachments/assets/13736dfa-1634-4d18-b236-d56818916462)

so for this challenge we are given a certificate signing request. though i dont know anyhting about it. so searched up google what is CSR.

```
-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF82OTNm
N2MwM30xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAPp+XuDB3ZkmrkvAsgtjP+mjIcYDWfptuZsJieu6eRl39wl4Sg38
+/OfY24LV9sNmgKyTGvpmCaUoZMYkvkulYSoFzE0xqPBo6kruLEyIvqqpAFqRH2b
mierLT6RcKgJHYr/Vt6SwP8NCCawCrvhQ4NZcuB49Hr/2AiGHzmf86/lG/c+lhmH
gyqPb1kDghsVxi/GNs9i7AgniZikqT8OTp0INmmCgZtJn1Jo615Iu/tFiC8Sfhhg
QHmTDLjgx1oP1kvZV2PE5UUN/oC05Zup8f31LksXZwpazZKwYC/LbN96HdqgVQ9K
S8e/4I7MJQmPmLIsLp3sdL2FiDGML3smAi0CAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAOxSR8Fs
Tdjfu9e0vRNqKWd09ISmYDQc3qnSbLRlYZyMK4pguALq310h/1nNgURWESbNJPOp
FkBWG0XWhWyWP7rTqxo/pk9AKx0TNbHDrS6KiBnKPq0mxjPZsH1L7wNYDc5OANDl
btvn3zT7lMms6z1qM7xUWXR76n2xL/81cdF725nBZ00mWmPW0S1pSmA4EEHCEgNW
0vWQqsIDki3gYc4NCm8OHjx79kcwE+ksyc6vHgMOwsYoOFJnyayhl15oN/3x7hW3
G1xovPupABpfOSNOcTwbgfrfjUDOLx/wirvj9L1N5EGDh4FOLaRZDs+tMrimGBBS
zGU13BnykmQ5jOQ=
-----END CERTIFICATE REQUEST-----

```
so i found the wikipedia page and gone through the website to find what kind of encoding this is 

Firstly, i thought it was Base64 encoded however when i used a online decoder. I was wrong.

Then dove deeper into the website and found out that its encoded as ASN-1. I used a online ASN-1 decoder.

```
SEQUENCE
    SEQUENCE
        INTEGER: 0
        SEQUENCE
            DER SET
                SEQUENCE
                    OBJECTIDENTIFIER: 2.5.4.3 (commonName)
                    UTF8String: picoCTF{read_mycert_693f7c03}
            DER SET
                SEQUENCE
                    OBJECTIDENTIFIER: 2.5.4.41 (2.5.4.41)
                    UTF8String: ctfPlayer
        SEQUENCE
            SEQUENCE
                OBJECTIDENTIFIER: 1.2.840.113549.1.1.1 (rsa-Encryption)
                NULL
            BIT STRING: 
0x 30 82 01 0A 02 82 01 01 00 FA 7E 5E E0 C1 DD 99 26 AE 4B C0 B2 0B 63 3F E9 A3 21 C6 03 59 FA 6D B9 9B 09 89 EB BA 79 19 77 F7 09 78 4A 0D FC FB F3 9F 63 6E 0B 57 DB 0D 9A 02 B2 4C 6B E9 98 26 94 A1 93 18 92 F9 2E 95 84 A8 17 31 34 C6 A3 C1 A3 A9 2B B8 B1 32 22 FA AA A4 01 6A 44 7D 9B 9A 27 AB 2D 3E 91 70 A8 09 1D 8A FF 56 DE 92 C0 FF 0D 08 26 B0 0A BB E1 43 83 59 72 E0 78 F4 7A FF D8 08 86 1F 39 9F F3 AF E5 1B F7 3E 96 19 87 83 2A 8F 6F 59 03 82 1B 15 C6 2F C6 36 CF 62 EC 08 27 89 98 A4 A9 3F 0E 4E 9D 08 36 69 82 81 9B 49 9F 52 68 EB 5E 48 BB FB 45 88 2F 12 7E 18 60 40 79 93 0C B8 E0 C7 5A 0F D6 4B D9 57 63 C4 E5 45 0D FE 80 B4 E5 9B A9 F1 FD F5 2E 4B 17 67 0A 5A CD 92 B0 60 2F CB 6C DF 7A 1D DA A0 55 0F 4A 4B C7 BF E0 8E CC 25 09 8F 98 B2 2C 2E 9D EC 74 BD 85 88 31 8C 2F 7B 26 02 2D 02 03 01 00 01 :0 unused bit(s)
        [0]
            DER SEQUENCE
                OBJECTIDENTIFIER: 1.2.840.113549.1.9.14 (1.2.840.113549.1.9.14)
                DER SET
                    DER SEQUENCE
                        DER SEQUENCE
                            OBJECTIDENTIFIER: 2.5.29.37 (extKeyUsage)
                            DER OCTET STRING: 300a06082b06010505070302
    SEQUENCE
        OBJECTIDENTIFIER: 1.2.840.113549.1.1.11 (SHA-256-WITH-RSA)
        NULL
    BIT STRING: 
0x EC 52 47 C1 6C 4D D8 DF BB D7 B4 BD 13 6A 29 67 74 F4 84 A6 60 34 1C DE A9 D2 6C B4 65 61 9C 8C 2B 8A 60 B8 02 EA DF 5D 21 FF 59 CD 81 44 56 11 26 CD 24 F3 A9 16 40 56 1B 45 D6 85 6C 96 3F BA D3 AB 1A 3F A6 4F 40 2B 1D 13 35 B1 C3 AD 2E 8A 88 19 CA 3E AD 26 C6 33 D9 B0 7D 4B EF 03 58 0D CE 4E 00 D0 E5 6E DB E7 DF 34 FB 94 C9 AC EB 3D 6A 33 BC 54 59 74 7B EA 7D B1 2F FF 35 71 D1 7B DB 99 C1 67 4D 26 5A 63 D6 D1 2D 69 4A 60 38 10 41 C2 12 03 56 D2 F5 90 AA C2 03 92 2D E0 61 CE 0D 0A 6F 0E 1E 3C 7B F6 47 30 13 E9 2C C9 CE AF 1E 03 0E C2 C6 28 38 52 67 C9 AC A1 97 5E 68 37 FD F1 EE 15 B7 1B 5C 68 BC FB A9 00 1A 5F 39 23 4E 71 3C 1B 81 FA DF 8D 40 CE 2F 1F F0 8A BB E3 F4 BD 4D E4 41 83 87 81 4E 2D A4 59 0E CF AD 32 B8 A6 18 10 52 CC 65 35 DC 19 F2 92 64 39 8C E4 :0 unused bit(s)
```
this was the decoded CSR. and flag was in this.

```
picoCTF{read_mycert_693f7c03}

```
# 7) Rotation-

For this challenge we are given with encrypted text which seems to be like the flag.

```
xqkwKBN{z0bib1wv_l3kzgxb3l_7l140864}
```
so i tried the dcode.fr tool to decode it.
Hint given was that ciphered using Rotation

so tried each ROT and got a match at ROT8.

```
picoCTF{r0tat1on_d3crypt3d_7d140864}
```




