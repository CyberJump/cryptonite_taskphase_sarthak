
# Practising Piping-

# Redirecting Output-

symbol > is used to redict the result of a command to the redirected file.For this challenge,we have redirect the PWN to file COLLEGE.

```bash
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{ExpqEnFtMwkFPRIOSBQ13O2_noZ.dRjN1QDLzkTN0czW}
```
# Redirecting more output-

We will still use  > to redict the output of command /challenge/run to /myflag.

```bash
Connected!
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{odRZT6ZKJqaW_b2BJaAZiO88zRM.dVjN1QDLzkTN0czW}
```
# Appending output-

To append the output of a command to redirected file, we use >> rather than > because > primarily deletes all contents then redirects the output of command however >> adds the output to the file without deleting the contents.

```bash
Connected!
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{sH59LVPpGESkKq2kZi4qSxORLA3.ddDM5QDLzkTN0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!
```
# Redirecting Errors-

We can use 2> to redirect errors of a command  to a different file and we can also redirect multiple file descriptors at the same time.For this challenge we have to firstly redict the output of /challenge/run to myflag and also redirect the errors to a file called instructions.
```bash
Connected!
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{w20Q8dmbY3pm2fQg-Ttduhq0uxs.ddjN1QDLzkTN0czW}

```
# Redirecting Inputs-

We can redirect the input for a command from a file to the command by using <.For this challenge we have to first redirect the value COLLEGE to a file PWN and then redirect the content of the file PWN to /challenge/run to get the flag.
```bash
Connected!
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{wkW56LFFh2RcUuZTdhNXu_Mn3Ix.dBzN1QDLzkTN0czW}
```
# Grepping stored results-

We have to use grep command to search for file in the data. For this challenge we ahev to redirect the output of /challenge/run command to a file /tmp/data.txt and then use grep function to find the flag from the heaps of data.
```bash
Connected!
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{o6RkAzZ6zo_VClCzcDdZgrNswnK.dhTM4QDLzkTN0czW}
```
# Grepping Live Outputs-

We use this using the | (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. We use this complete this challenge by running the /challenge/run command and also grepping for the flag in form of pwn.collge.
```bash
Connected!
Connected!
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{wxt6fZXAw38-621-WaRYfhsniOa.dlTM4QDLzkTN0czW}
```
# Grepping Errors -

We dont have direct way of redireting errors to a files then grep it using piping, however we can use >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|). 
```bash
Connected!
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{QTIZe76FEZurBvx712yEOzrQmtN.dVDM5QDLzkTN0czW}
```
# Duplicating piped data with tee-

Tee can be used to duplicate the output data of command while its being piped to a different command.In this challenge we have to pipe the /challenge/pwn which contains a secret code to /challenge/college with the correct code. For this we first intercept the data being piped via tee to a file then cat the file to get the secret code after which we pipe the command output with correct secret code argument to /challenge/college.
```bash
Connected!
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee data.txt | /challenge/college
Processing...
WARNING: you are overwriting file data.txt with tee's output...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat data.txt
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "ANfdHavF"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret ANfdHavF| /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{ANfdHavFXP7BAcQXPQ_tA29MbVu.dFjM5QDLzkTN0czW}
```
# Writing to multiple programs -

We can redirect the stdout of a command to stdin of multiple programs using >() function. We can use tee to redirect the stdout to >(/challenge/the) and redirect the other copy to /challenge/planet as stdin.
```bash
Connected!
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{gUCxuuzcWGVPuYkl47-iiAxlUpn.dBDO0UDLzkTN0czW}
```
# Writing to multiple programs -

We can redirect the stdout of a command to stdin of multiple programs using >() function. We can use tee to redirect the stdout to >(/challenge/the) and redirect the other copy to /challenge/planet as stdin.
```bash
Connected!
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{gUCxuuzcWGVPuYkl47-iiAxlUpn.dBDO0UDLzkTN0czW}
```
# Split-piping stderr and stdout - 

we have to split the stderr and stdout from one another. For this we have use > because | will link stdout and stdin of the commands. Firstly we redirct the stdout of /challenge/hack to a named pipe of /dev/fd/63 which will then pipe this to /challenge/planet and for stderr we will take the same approach for but use 2> to redirect only the errors.

```bash 
connected!
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{g9MwcIe1nPUthME_hjbxGIL2Wp3.dFDNwYDLzkTN0czW}
```









