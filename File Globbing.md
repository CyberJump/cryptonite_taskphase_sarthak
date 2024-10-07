
# File Globbing

# Matching with *-

For this challenge we have to change our directory from /home/hacker to /challenge then run /challenge/run. however, we have keep the cd command argument not more than 4 characters so we use * to cd and run/challenge/run.

```bash
Connected!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{g01X750DGAPShj1WE5FntpXO5zu.dFjM4QDLzkTN0czW}
```
# Matching with *-

? works as a single character wildcard.For this challenge we have to change directory to /challenge by using ? for c and l then run the command /challenge/run.

```bash
Connected!
This challenge resets your working directory to /home/hacker unless you change
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{wmz49YGUdz4neLeOZj8UAaROITv.dJjM4QDLzkTN0czW}
```
# Matching with [ ]-

[] works as a single character wildcard but for the subset of those characters.For this challenge we have to change directory to /challenge/files and then run the command /challenge/run with the argument files_[bash] which will glob for file_b,file_a,file_s and file_h.

```bash
Connected!
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{omj_w7sxlysN3j2uFRs2zx-mwxt.dNjM4QDLzkTN0czW}
```
# Mixing Globs-

we have [],* and ? for globbing of files.In this challenge, we have to use these gloobing methods to find the specific three files (that are "challenging", "educational", and "pwning") in the given directory /challenge/files. we use [cep]* to search for the first letters of files and return the files.
```bash
Connected!
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{ADbQCXmJkO0dzQ_Zo5T8tM1qGQ1.dVjM4QDLzkTN0czW}
```
# Exclusionary Globbing-

upon using ! or ^ before [] gives you exclusionary globbing and return all files except the one that satisfy [] condition. For this challenge, we have to use this property of globbing to find all files except the ones which start with p,w or n. we will use [!pwn]* this will return all files not starting with p,w or n.
```bash
Connected!
Connected!
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{AMffO66hwHr7iklhk94flvOjV9k.dZjM4QDLzkTN0czW}
```




