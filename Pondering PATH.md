
# Pondering PATH -

# The Path Variable-

The shell variable PATH stores the required data to invoke shell commands which can be easily disturbed by changing the value of PATH variable.In this challenge. we blank the PATH variable and run /challenge/run.

```bash
Connected!
hacker@path~the-path-variable:~$ PATH=''
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{AfOLtgvV_jdwsIr29fl-wnakm3V.dZzNwUDLzkTN0czW}
```
# Setting PATH-

we can overwrite PATH variable with a directory to make the scripts or commands present in that directory executable just by barename.For this challenge we have to change the PATH with directory of win command and run /challenge/run.

```bash
Connected!
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{M5mcTy7wzK1u1C1_d8z5zEpV4_V.dVzNyUDLzkTN0czW}
```
# Adding Commands-

This challenge is a tricky challenge as we have to first create a shell script win.sh with cat/flag command in it but also give change its permission to be executable by chmod after which we have to rename it to win so that it could be executable command win.Now we append the PATH variable by adding the directory of win in it, and then when we run /challenge/run we will get the flag.
```bash
Connected!
hacker@path~adding-commands:~$ touch win.sh
hacker@path~adding-commands:~$ nano win.sh
hacker@path~adding-commands:~$ mv win.sh win
hacker@path~adding-commands:~$ chmod ugo+rwx win
hacker@path~adding-commands:~$ PATH=$PATH:/home/hacker
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{Mq0cUGMy1Ilm2ksIeXgjgfT1wsY.dZzNyUDLzkTN0czW}
```
