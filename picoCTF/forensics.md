# FORENSICS

# Trivial Flag Transfer Protocol

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