# FORENSICS

# 1)Trivial Flag Transfer Protocol

So When we open the challenge we are given with a PCAPNG file.
so searched up whats a pcapng file and found out its packet capture file and we can analyse it using wireshark
![image](https://github.com/user-attachments/assets/9968aada-f8d2-4d76-86aa-1d81d711d260)

so well i opened the file in wireshark and damn i couldnt understand anything. i mean thats pretty obvious because i havent ever used wireshark. so pulled up youtube and learnt about how to analyse a pcap file in wireshark
![image](https://github.com/user-attachments/assets/7288850c-f1c5-4565-9176-2af2092ba1a3)
this is how the capture file looked like in wireshark

The video I referred to understand this-
https://www.youtube.com/watch?v=ZNS115MPsO0&list=PLW8bTPfXNGdC5Co0VnBK1yVzAwSSphzpJ&index=8

It was a great video, and I understood how to use statics section of wireshark.

![image](https://github.com/user-attachments/assets/ef34858e-4ccb-48d3-a32d-083cb856d0b1)

well ya, i think this was a wrong tangent because i was stuck here for like an hour figuring out what to do next.\
so I was like i need to try to extract the files that were transferred here and luckily for me the same youtuber had the video to extract file from a PCAP file next in his playlist :)\
video link- https://www.youtube.com/watch?v=Fn__yRYW6Wo&list=PLW8bTPfXNGdC5Co0VnBK1yVzAwSSphzpJ&index=9

so then i followed the tutorial and got the files that were transferred.

![image](https://github.com/user-attachments/assets/34419a6a-0154-4083-be1f-52960dbff97b)

okkk so i exported the files to a folder and access them.\
There was 1)Instruction.txt file which was a txt file containing a string of &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;letters\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2)Plan file which i opened with notepad to find a string of letters\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3)Program.deb file which i didnt know what it was\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4) Three BMP file pictures and well from the BMP i got it this &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picture contains something hidden.

![image](https://github.com/user-attachments/assets/9d0b0f07-9b5e-4212-8664-dc1f57222ff4)

well i was kinda stuck here, but then imma come clean and admit i used GPT to identify which kind of encryption was used in txt files (that are instruction.txt and plan file).
![image](https://github.com/user-attachments/assets/8595ecad-96c7-43f7-a8a8-6f90da09feef)

well atleast i found out that its ROT13 so i used a online decoder to find the decoded content of first file-
![image](https://github.com/user-attachments/assets/de1c1fc0-df33-40f1-af56-4ab6beb00c4b)

The decoded text didnt make sense at first but then I spaced out the words and I got this- TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN\
Which well first tells that the TFTP isnt safe and also that i should decrypt the plan file.

I did the same thing for the plan file too and got-
I USED THE PROGRAM AND HID IT WITH-DUEDILIGENCE.CHECK OUT THE PHOTOS

so now i used my Ubuntu WSL to install the .deb file and got that they used Steghide to hide the flag in the pictures.

Ahhhhh now i had to learn how to use another software. T_T\
This challenge is testing me hard.

Well i tried to install it and got into some problem but worked past it using a youtube video to define the steghide file folder as PATH in windows so that i can use it as a variable in cmd prompt.\

Link - https://www.youtube.com/watch?v=CYjc3Ib12EQ



![image](https://github.com/user-attachments/assets/2785a58b-61f3-4444-8160-3bb055852509)

I opened CMD prompt and ran the steghide command to extract data from the image. Even though i knew that steghide needs a paraphrase to first hide it and also that is used to decode it.\
After pondering upon it i read the decrypted text from PLAN file and bam i got it the paraphrase was DUEDILIGENCE

Then i entered the paraphrase and voila a flag.txt file was downloaded on my system.

![image](https://github.com/user-attachments/assets/01cb1b57-81d3-4b52-9e7d-810edfca27f0)

Yess finally i got it and i opened to the text file to get the flag that was- picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}

Wooooow that was a long and strenuos chall to first understand wireshark and then steghide.

BUT at the end the flag gave me the adrenaline rush required 🤠

# 2)Tunn3l_v1s10n

In this challenge we are given with a file and we have to recover the flag from that file. 

![Screenshot_2024-12-13_14_30_39](https://github.com/user-attachments/assets/37a10f9a-77fb-49a7-b4d5-39707bce15ab)

so i downloaded the file on my storage and tried to check what kinda file it is

```
┌──(kali㉿kali)-[~]
└─$ cd ./Downloads    
                                                                                                                                                                                                                                           
┌──(kali㉿kali)-[~/Downloads]
└─$ file tunn3l_v1s10n
tunn3l_v1s10n: data
```
looks like the file has some issue, so tired to check the metadata of the file

```
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool tunn3l_v1s10n
ExifTool Version Number         : 12.76
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2024:12:13 14:42:52+05:30
File Access Date/Time           : 2024:12:13 14:42:52+05:30
File Inode Change Date/Time     : 2024:12:13 14:42:52+05:30
File Permissions                : -rw-rw-r--
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347
```
looks like it is a BMP file meaning it was to contain some kind of image. i tred to open the image.

![Screenshot_2024-12-13_14_47_34](https://github.com/user-attachments/assets/f870af98-bb5a-46b8-8897-2c5c7a6e05c4)

ok looks like there some header issue in the image. At this time, i was clear that i have to hexedit the image to recover it.

well unlucky for me i didnt know anything about BMP file signature so searched up web and got greatt sources to help me.

source 1-https://www.file-recovery.com/bmp-signature-format.html \
source 2-http://www.ece.ualberta.ca/~elliott/ee552/studentAppNotes/2003_w/misc/bmp_file_format/bmp_file_format.html 

This sources helped understand whats actually happening in the hexdecimal form of this image.

i did the hexedit command on the file and woahhhh got a hugeee map of hexdecimals 

```
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 BA D0  00 00 6E 04  00 00 32 01  00 00 01 00  18 00 00 00  00 00 58 26  2C 00 25 16  00 00 25 16  00 00 00 00  00 00 00 00  BM.&,.............n...2...........X&,.%...%.........
00000034   00 00 23 1A  17 27 1E 1B  29 20 1D 2A  21 1E 26 1D  1A 31 28 25  35 2C 29 33  2A 27 38 2F  2C 2F 26 23  33 2A 26 2D  24 20 3B 32  2E 32 29 25  30 27 23 33  2A 26 38 2C  ..#..'..) .*!.&..1(%5,)3*'8/,/&#3*&-$ ;2.2)%0'#3*&8,
00000068   28 36 2B 27  39 2D 2B 2F  26 23 1D 12  0E 23 17 11  29 16 0E 55  3D 31 97 76  66 8B 66 52  99 6D 56 9E  70 58 9E 6F  54 9C 6F 54  AB 7E 63 BA  8C 6D BD 8A  69 C8 97 71  (6+'9-+/&#...#..)..U=1.vf.fR.mV.pX.oT.oT.~c..m..i..q
0000009C   C1 93 71 C1  97 74 C1 94  73 C0 93 72  C0 8F 6F BD  8E 6E BA 8D  6B B7 8D 6A  B0 85 64 A0  74 55 A3 77  5A 98 6F 56  76 52 3A 71  52 3D 6C 4F  40 6D 52 44  6E 53 49 77  ..q..t..s..r..o..n..k..j..d.tU.wZ.oVvR:qR=lO@mRDnSIw
000000D0   5E 54 53 39  33 70 58 52  76 61 59 73  5F 54 7E 6B  5E 86 74 63  7E 6A 59 76  62 50 76 5E  4C 7A 62 50  87 6D 5D 83  69 59 8D 73  63 9B 81 71  9E 84 74 98  7E 6E 9B 81  ^TS93pXRvaYs_T~k^.tc~jYvbPv^LzbP.m].iY.sc..q..t.~n..
00000104   71 8D 73 63  73 5A 4A 70  57 47 5A 41  31 4F 36 26  4E 37 27 4F  38 28 4F 38  28 51 3A 2A  50 39 29 4F  38 29 4B 35  29 50 3A 2F  4B 35 2A 3F  29 1E 42 2E  23 4B 37 2C  q.scsZJpWGZA1O6&N7'O8(O8(Q:*P9)O8)K5)P:/K5*?).B.#K7,
00000138   45 31 26 3F  2B 20 43 2F  24 43 2F 24  40 2A 1F 48  32 27 4B 32  28 47 2E 24  40 27 1D 45  2C 22 4C 34  28 4C 34 28  4B 33 27 4A  32 26 4C 32  24 4E 34 26  50 35 27 52  E1&?+ C/$C/$@*.H2'K2(G.$@'.E,"L4(L4(K3'J2&L2$N4&P5'R
0000016C   37 29 53 36  28 55 38 2A  4B 30 22 5D  42 34 63 49  39 49 2F 1F  44 2B 1B 4D  34 24 4D 36  27 4A 33 24  46 2C 20 48  2E 22 46 2E  22 44 2E 22  3C 26 1B 32  20 15 30 1F  7)S6(U8*K0"]B4cI9I/.D+.M4$M6'J3$F, H."F."D."<&.2 .0.
000001A0   16 32 23 1A  36 27 1E 3C  2B 22 3E 2B  24 42 2C 26  5E 44 3E 66  4C 46 36 1D  19 33 1F 1A  3F 30 2D 13  0A 06 09 06  02 05 04 00  0A 05 04 0B  06 05 0D 05  05 0B 06 05  .2#.6'.<+">+$B,&^D>fLF6..3..?0-.....................
000001D4   0A 06 05 08  06 05 08 06  05 0A 06 05  0D 05 05 0D  05 05 0B 03  04 06 00 01  05 00 00 09  04 03 0B 06  03 0A 05 02  08 05 01 09  06 02 09 06  02 07 04 00  07 04 00 08  ....................................................
00000208   05 01 08 04  03 06 02 01  06 01 02 07  02 03 06 04  03 04 02 01  06 02 01 06  02 01 05 00  00 1D 18 17  1C 15 12 0E  07 04 14 0B  07 16 0D 09  15 0D 06 17  0F 08 1B 13  ....................................................
0000023C   0C 10 08 01  12 0B 02 16  0F 06 17 0E  05 16 0D 04  16 0D 04 17  0E 05 1A 11  08 16 0D 04  1C 14 0D 1F  17 10 28 20  19 22 1A 13  20 17 13 1B  12 0E 18 0F  0B 15 0C 08  ..................................( .".. ...........
00000270   12 09 05 16  0D 09 15 0C  08 11 08 04  15 0C 08 13  0A 06 0F 06  02 12 09 05  12 0C 07 13  0D 08 11 0B  06 11 0B 06  10 0A 05 10  0A 05 0F 09  04 0E 08 03  0B 07 02 0B  ....................................................
000002A4   07 02 0A 05  02 08 03 00  08 03 00 06  01 00 0A 05  04 08 03 02  08 04 03 05  01 00 05 01  00 08 04 03  04 02 01 02  00 00 05 03  02 04 02 01  02 00 00 04  02 02 03 01  ....................................................
000002D8   01 04 02 01  04 02 01 06  06 00 09 06  01 0A 08 00  0C 08 03 0C  08 03 0D 08  07 0B 06 05  0D 05 05 10  08 08 12 09  06 11 08 04  11 08 04 13  0B 04 16 0F  06 0F 08 00  ....................................................
0000030C   13 0C 03 1B  14 0B 1B 14  0B 11 0A 01  16 0F 06 15  0E 05 18 11  08 16 0F 06  10 09 00 16  0F 06 16 0F  06 14 0D 04  0E 07 00 14  0D 04 17 0F  08 16 0E 07  14 0C 05 1B  ....................................................
00000340   13 0C 1E 16  0F 19 11 0A  19 0F 08 14  0A 03 17 0D  06 18 0E 07  18 0E 07 17  0D 06 16 0C  05 17 0D 06  1A 10 09 1C  12 0B 1A 11  0E 18 0F 0C  20 17 14 19  10 0D 11 08  ............................................ .......
00000374   05 15 0C 09  13 0A 07 14  0B 08 14 0B  08 16 0D 0A  17 0B 09 15  09 07 1B 0F  0D 17 0B 09  15 09 07 13  07 05 1C 10  0E 18 0C 0A  16 0A 08 17  0B 09 16 0A  08 15 09 07  ....................................................
000003A8   13 0A 07 16  0D 0A 11 08  05 14 0B 08  17 0E 0A 16  0D 09 13 0A  06 11 08 04  14 0B 07 17  0E 0A 1A 0F  0B 1F 14 10  17 0D 06 1F  15 0E 27 1D  16 1B 11 0A  1C 13 0A 16  ..........................................'.........
000003DC   0D 04 18 0F  06 18 0F 06  1A 10 09 1E  14 0D 1F 15  0E 1F 15 0E  1B 10 0C 27  1C 18 20 16  0F 22 18 11  24 1A 13 28  1E 17 31 27  20 2B 21 1A  1D 12 0E 21  16 12 1D 12  .......................'.. .."..$..(..1' +!....!....
00000410   0E 22 17 13  25 1A 16 1D  12 0E 13 08  04 14 09 05  17 0C 08 14  09 05 1E 13  0F 28 1D 19  2D 22 1E 32  27 23 27 1C  18 21 16 12  20 18 11 26  1E 17 21 19  12 18 10 09  ."..%....................(..-".2'#'..!.. ..&..!.....
00000444   25 1D 16 1C  14 0D 1A 12  0B 1B 13 0C  2E 26 1F 35  2D 26 3E 36  2F 37 2F 28  2E 25 21 32  29 25 39 30  2C 48 3F 3B  47 3E 3B 23  1A 17 2B 22  1E 34 2B 27  2F 24 20 2F  %............&.5-&>6/7/(.%!2)%90,H?;G>;#..+".4+'/$ /
00000478   24 20 30 26  1F 2B 21 1A  26 1D 14 2C  23 1A 33 28  20 2D 22 1A  28 1D 15 21  16 0E 26 1B  13 24 19 11  1B 10 08 1A  0F 07 19 0E  06 20 15 0D  2F 24 1C 2E  23 1B 2D 22  $ 0&.+!.&..,#.3( -".(..!..&..$........... ../$..#.-"
000004AC   1A 29 1E 16  22 17 0F 20  15 0D 29 1D  13 2A 1E 14  32 26 1C 2D  21 17 31 25  1B 34 28 1E  36 2A 20 38  2C 22 3A 2E  24 31 25 1B  2A 1C 10 2D  1F 13 2B 1D  11 2F 21 15  .)..".. ..)..*..2&.-!.1%.4(.6* 8,":.$1%.*..-..+../!.
000004E0   39 2B 1F 49  3B 2F 49 3B  2F 38 2A 1E  3E 30 24 3D  2F 23 32 24  18 3E 30 24  4C 3E 32 39  2B 1F 37 29  1D 41 33 27  3D 2F 23 3A  2C 20 2B 1D  11 24 16 0A  1C 0E 02 22  9+.I;/I;/8*.>0$=/#2$.>0$L>29+.7).A3'=/#:, +..$....."
00000514   14 08 28 18  11 2D 1D 16  24 17 0F 32  25 1D 49 3B  35 13 05 00  46 3A 36 2F  23 1F 32 26  22 35 29 25  23 19 12 2C  22 1B 3B 32  29 3D 34 2B  33 2A 21 2A  21 18 2D 24  ..(..-..$..2%.I;5...F:6/#.2&"5)%#..,".;2)=4+3*!*!.-$
00000548   1A 32 29 1F  2B 22 18 23  1A 10 24 1B  11 2D 24 1A  41 38 2E 2D  24 1A 29 20  16 2B 22 18  2A 21 17 37  2E 24 2D 24  1A 2E 25 1B  34 2B 21 37  2E 24 42 38  2E 3E 34 2A  .2).+".#..$..-$.A8.-$.) .+".*!.7.$-$..%.4+!7.$B8.>4*
0000057C   22 18 0E 2A  20 16 2D 23  19 37 2D 23  30 26 1C 37  2D 23 2D 23  19 26 1C 12  1F 15 0B 35  2B 21 27 1D  13 3F 35 2B  35 2B 21 38  2E 24 2C 22  1B 2C 22 1B  2E 22 1C 31  "..* .-#.7-#0&.7-#-#.&.....5+!'..?5+5+!8.$,".,"..".1
000005B0   25 1F 2A 1E  18 2F 23 1D  31 25 1F 32  26 20 2F 23  1D 27 1B 15  3C 2E 28 27  19 13 23 15  0F 57 49 43  3D 2F 29 3F  31 2B 45 38  36 3D 31 2D  3F 33 2D 46  3A 30 4D 3F  %.*../#.1%.2& /#.'..<.('..#..WIC=/)?1+E86=1-?3-F:0M?
000005E4   33 55 44 37  5E 47 38 69  4E 40 93 70  63 66 3F 31  70 44 37 87  5B 4A C7 99  87 C2 96 7F  6E 44 2D 96  6D 54 B6 88  70 BC 8D 71  AE 7E 5C DD  AC 84 DE AE  84 DC AD 81  3UD7^G8iN@.pcf?1pD7.[J......nD-.mT..p..q.~\.........
00000618   D8 AB 80 D5  A8 7D ED BA  92 DE AB 83  D0 9A 71 D0  9C 74 CA 97  76 A5 77 58  98 6E 57 9D  7A 66 78 5A  47 61 47 36  5A 42 30 71  59 47 6F 57  43 6F 57 43  7E 66 52 62  .....}........q..t..v.wX.nW.zfxZGaG6ZB0qYGoWCoWC~fRb
0000064C   4A 36 71 59  45 65 4D 39  7D 62 4E 7D  62 4E 7E 61  4C 7E 61 4C  84 65 50 80  61 4C 91 6E  5A 91 6E 5A  8D 6B 54 84  62 4A 7F 5D  45 7D 5C 42  83 61 44 79  57 3A 7D 5B  J6qYEeM9}bN}bN~aL~aL.eP.aL.nZ.nZ.kT.bJ.]E}\B.aDyW:}[
00000680   3D 8E 6C 4E  89 67 49 86  64 46 8A 68  4A 86 64 46  88 66 48 87  65 47 91 6E  54 92 6F 55  91 6D 55 98  74 5C 90 6E  57 91 6F 58  91 70 5C 8D  6C 58 90 71  5C 8A 6B 56  =.lN.gI.dF.hJ.dF.fH.eG.nT.oU.mU.t\.nW.oX.p\.lX.q\.kV
000006B4   8F 70 5B 8C  6D 58 89 6C  57 82 65 50  81 64 4F 87  6A 55 85 6A  55 83 68 53  86 69 54 87  6A 55 8A 6B  54 90 71 5A  95 76 5D 91  72 59 95 74  5A 93 72 58  98 73 57 9A  .p[.mX.lW.eP.dO.jU.jU.hS.iT.jU.kT.qZ.v].rY.tZ.rX.sW.
000006E8   75 59 A1 7B  5D A9 83 65  A2 7C 5E 9D  77 57 A7 7E  5E A7 7E 5D  A4 7C 59 95  6D 4A 9E 77  51 9B 74 4E  9A 72 4F 9F  77 54 A3 7A  5A 9F 76 56  A4 78 5B A4  78 59 A5 7A  uY.{]..e.|^.wW.~^.~].|Y.mJ.wQ.tN.rO.wT.zZ.vV.x[.xY.z
0000071C   59 A0 76 51  A8 7E 59 B3  88 61 B7 89  60 B4 86 5D  B8 8B 66 B6  8C 69 92 6C  4C 70 4E 31  77 58 3F 71  54 3F 64 4B  37 68 50 3E  56 3F 30 57  40 31 58 41  32 5F 48 39  Y.vQ.~Y..a..`..]..f..i.lLpN1wX?qT?dK7hP>V?0W@1XA2_H9
00000750   59 3F 31 52  3B 2C 58 40  34 5F 49 3D  55 40 31 53  3E 2F 52 3E  2D 52 3E 2D  54 40 2F 5D  49 38 5D 46  36 5E 47 37  54 3D 2D 59  42 32 5C 45  36 40 29 1A  3E 26 1A 4D  Y?1R;,X@4_I=U@1S>/R>-R>-T@/]I8]F6^G7T=-YB2\E6@).>&.M
00000784   35 29 57 3F  33 53 3B 2F  58 40 34 4D  35 29 57 3F  33 4C 34 28  51 39 2D 5C  44 38 4D 37  2B 4F 39 2D  53 3D 31 4A  34 28 54 3E  32 50 3A 2E  4E 38 2C 54  3E 32 49 33  5)W?3S;/X@4M5)W?3L4(Q9-\D8M7+O9-S=1J4(T>2P:.N8,T>2I3
000007B8   27 3E 28 1C  57 41 35 4B  35 29 4D 37  2B 5C 46 3A  4A 34 28 5A  44 38 5E 48  3C 4C 36 2A  44 2E 22 44  2E 22 4C 36  2A 3B 25 19  4A 34 28 52  3C 30 4A 34  29 46 30 25  '>(.WA5K5)M7+\F:J4(ZD8^H<L6*D."D."L6*;%.J4(R<0J4)F0%
000007EC   4B 37 2C 49  35 2A 3A 26  1B 44 30 25  47 33 28 3E  2A 1F 45 33  28 3B 29 1E  38 28 1C 4D  3D 31 58 48  3C 3A 2A 1E  40 30 24 62  52 46 38 2A  1E 3B 2D 21  4D 41 35 6B  K7,I5*:&.D0%G3(>*.E3(;).8(.M=1XH<:*.@0$bRF8*.;-!MA5k
00000820   5F 53 6F 63  59 4D 41 37  45 3B 31 47  3D 33 47 3C  34 49 3E 36  47 3E 35 4D  44 3B 56 4C  45 55 4B 44  53 49 42 3A  30 29 5B 52  49 57 4E 45  53 4A 41 51  48 3F 4D 44  _SocYMA7E;1G=3G<4I>6G>5MD;VLEUKDSIB:0)[RIWNESJAQH?MD
00000854   3B 55 4C 43  5F 56 4D 55  4C 43 31 28  1F 62 59 50  50 47 3E 4C  43 3A 56 4D  44 4D 44 3B  54 4B 42 4A  41 38 56 4C  45 53 49 42  67 5D 56 6E  64 5D 66 5A  54 45 39 33  ;ULC_VMULC1(.bYPPG>LC:VMDMD;TKBJA8VLESIBg]Vnd]fZTE93
00000888   4B 3F 39 54  48 42 5C 50  4A 4E 42 3C  70 66 5F 54  4A 43 48 40  39 63 5B 54  3C 36 2F 49  43 3C 67 5D  56 42 3A 33  50 48 41 5A  54 4D 59 55  50 52 4E 49  48 42 3D 45  K?9THB\PJNB<pf_TJCH@9c[T<6/IC<g]VB:3PHAZTMYUPRNIHB=E
000008BC   3F 3A 4E 43  3F 4B 40 3C  5B 4F 49 66  5A 54 43 3A  31 70 67 5E  73 6C 63 66  61 58 7C 7C  76 68 6A 64  4A 4B 47 69  6A 66 5A 5B  59 7C 7D 7B  7C 7C 7C 71  71 71 76 76  ?:NC?K@<[OIfZTC:1pg^slcfaX||vhjdJKGijfZ[Y|}{|||qqqvv
000008F0   76 73 73 73  7D 7D 7D 8D  8D 8D 6C 6D  6B 71 72 70  A3 A4 A2 69  6C 6A 91 95  96 6C 71 72  90 95 96 6F  74 75 7E 83  84 60 65 66  7F 84 85 88  8D 8E 7E 83  84 61 66 67  vsss}}}...lmkqrp...ilj...lqr...otu~..`ef......~..afg
00000924   77 7C 7D 6E  73 74 94 99  9A 73 78 79  A4 A9 AA 85  8A 8B 9F A7  A7 6D 75 75  55 5D 5D 6C  74 74 57 5C  5D 79 7E 7F  8B 90 91 83  88 89 8A 8F  92 6D 72 75  5E 63 66 4F  w|}nst...sxy.........muuU]]lttW\]y~..........mru^cfO
00000958   54 57 87 8A  8E 8C 8F 93  89 8C 90 7C  7F 83 89 8C  90 94 97 9B  6C 6F 73 56  59 5D 58 5C  5D 5A 5E 5F  43 47 48 4C  50 51 51 56  55 53 58 57  94 9A 99 8C  92 91 8D 94  TW.........|........losVY]X\]Z^_CGHLPQQVUSXW........
0000098C   91 9C A3 A0  9D A4 A1 90  97 94 7F 86  83 9E A5 A2  A5 AA A8 6D  72 70 63 68  66 53 58 56  6B 6E 6C 81  84 82 56 57  55 84 85 83  86 87 85 5C  5D 5B 5E 5C  5B 86 84 83  ...................mrpchfSXVknl...VWU......\][^\[...
000009C0   7E 7C 7B 70  6F 6B A7 A4  A0 9D 9A 95  A3 9F 9A 85  81 7C 77 6E  6A 9F 96 92  8E 84 7D 8C  82 7B 9C 92  8B 8F 85 7E  87 80 77 8B  84 7B 8D 88  7F 8F 8A 81  8A 88 7E 83  ~|{pok...........|wnj.....}..{.....~..w..{........~.
000009F4   81 77 97 91  8C 97 91 8C  90 8B 88 83  7E 7B 71 6E  6A 64 61 5D  55 51 50 56  52 51 52 4F  4B 82 7F 7B  7C 79 74 68  65 60 68 65  5D 67 64 5C  64 5E 57 6D  67 60 81 7A  .w..........~{qnjda]UQPVRQROK..{|ythe`he]gd\d^Wmg`.z
00000A28   71 8D 86 7D  84 7B 77 64  5B 57 7E 74  74 69 5F 5F  5B 54 51 58  51 4E 77 71  6C 66 60 5B  6F 69 62 6A  64 5D 63 5C  59 5B 54 51  6D 67 68 64  5E 5F 4D 45  45 6B 63 63  q..}.{wd[W~tti__[TQXQNwqlf`[oibjd]c\Y[TQmghd^_MEEkcc
00000A5C   69 61 61 5D  55 55 61 59  59 77 6F 6F  6F 67 67 55  4D 4D 6D 63  63 72 68 68  63 59 59 82  78 78 72 68  68 54 4A 4A  6A 60 60 63  59 59 69 5D  5D 6E 62 60  65 59 57 6B  iaa]UUaYYwoooggUMMmccrhhcYY.xxrhhTJJj``cYYi]]nb`eYWk
00000A90   60 5C 70 68  61 74 6C 65  60 5B 52 74  6F 66 5A 53  4A 76 6D 63  8B 7D 71 A8  95 86 BF A6  92 E7 C8 B1  F1 CC B2 F3  C9 AC F7 C9  A7 FE CC A8  F5 C3 9F F8  C6 A2 FA C9  `\phatle`[RtofZSJvmc.}q.............................
00000AC4   A3 FB CA A4  FC C9 A1 FD  CA A2 FC C8  A0 FC C8 A0  FC C8 A0 FC  C8 A0 FC C7  A2 FC C7 A2  FE C7 A2 FE  C7 A2 FF C7  A0 FF C7 A0  FF C6 9F FF  C6 9F FF C6  9F FF C6 9F  ....................................................
00000AF8   FF C6 9F FF  C6 9F FF C6  9F FF C6 9F  FF C6 9F FF  C6 9F FF C5  9E FF C5 9E  FF C5 9E FF  C5 9E FF C5  9E FF C5 9E  FF C5 9E FF  C5 9E FF C5  9E FF C5 9E  FF C5 9E FF  ....................................................
00000B2C   C5 9E FF C4  9D FF C4 9D  FF C4 9D FF  C4 9D FF C4  9D FF C4 9D  FF C4 9D FF  C4 9D FC C3  9C FC C3 9C  FC C3 9C FC  C3 9C FC C3  9C FC C3 9C  FC C3 9C FC  C3 9C FC C2  ....................................................
00000B60   9E FC C2 9E  FC C2 9E FC  C2 9E FC C2  9E FC C2 9E  FC C2 9E FC  C2 9E FC C2  9E FC C2 9E  FA C3 9E F9  C2 9D F6 C1  9C F6 C1 9C  FA C0 9C F9  BF 9B FC C1  9A FC C1 9A  ....................................................
00000B94   FE C0 9A FC  C1 9A FA C1  9A F6 C2 9A  F6 C2 9A F5  C2 9A F4 C1  99 F2 BF 97  F5 C3 99 F3  C2 96 F6 C1  96 F8 C4 96  F8 C1 96 F7  C2 97 F7 C0  99 F3 BF 9A  E9 BA 9A EF  ....................................................
---  tunn3l_v1s10n       --0x0/0x2C268E--0%---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```
okk so first issue with file was that it had unsupported header so i checked theBITMAPINFOHEADER size part of file and yaaa it way offffff then it should have been. The value should be 40 however here the value was 53434 !!!!.Thats pretttty high so what did was i changed the header size value to 28 00 00 00. tried to open the file and well it opened.

![Screenshot_2024-12-13_15_06_54](https://github.com/user-attachments/assets/f50ddfee-d5d7-4300-b3cb-3aad214955ee)

T-T wowww the image had notaflag{sorry}.....ahhhh well i was kinda stuck here and tried to look for something. I looked at the parts of hexdecimal and one by one checked each field, one field felt a bit off here , that was size of image data in bytes- 58 26 2C 00 which was equal to 2893400 bytes. Well nahh i was equal to 2.9 mb which i got in the metadata too. well i was stuck again......

Now i just started tinkering with image it self. so i tried to change the image height to make it a square image and well i think i got something there.
 so changed the image height attribute to 6E 04 00 00 same as the width of the image. The resultant image was- 
 ![Screenshot_2024-12-13_15_19_19](https://github.com/user-attachments/assets/2b7ba70e-6166-4775-86eb-599ff45481fe)

and at the top i can see the thing i needed the most the flag :)\
so flag is picoCTF{qu1t3_a_v13w_2020}

That was a greattt challenge.
# 3) m00nwalk-

Alright when i open up the challenge the i am given with a .wav audio file.

![image](https://github.com/user-attachments/assets/37c3e3d2-f555-468f-9980-2e90ecde1391)

the moment i got the file i noticed it had some different type of thing i cant explain it but it gave a hint to check the spectrography of audio.

So i check the spectrography of audio on audacity because in my previous CTFs i ahve found the flag in the spectrographs. However i found nothing in this case.

So i checked the hint which was how the images of moon where sent back to earth.

upon researching a bit about this I found that the images of moon where sent back using sstv singals in which images are sent as audio with headers and the main data.

Anyways now that i know about it I searched up the some softwares to decode sstv signals and found one called MMSSTV.quite an oldschool application.

![image](https://github.com/user-attachments/assets/4ebd9330-8f3c-4075-b094-425bc2596a62)

and woowwww this application is sooooo old and i ran into few issues with this application.
- Firstly I need to have the audio in .mmv format not .wav
- Secondly even After I tried to attempt to convert the .wav file to .mmv file.

Because of the above reasons i pretty much gave up and tried a different approach and searched youtube.

and i found a great video which helped me configure the application qsstv on my linux system and i followed the tutorial to configure it.

https://www.youtube.com/watch?v=-fAawZ5849Y&t=365s

after configuring it, I played the sound and the image was generated.

![image](https://github.com/user-attachments/assets/ba811e98-c835-4a62-bcd8-2d080775539a)

and flag was right in front of my eyes.

```
flag- picoCTF{beep_boop_im_in_space}

```

