
# Processes and Jobs-

# Listing Processes-

you can list out all the processes working in the terminal and by passing argument you can make this command working. for this challenge we have to find the challenge command running and relaunch it.

```bash
Connected!
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 12:15 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /ru
root           7       1  0 12:15 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 12:15 ?        00:00:00 /challenge/31489-run-10938
root          72      68  0 12:15 ?        00:00:00 sleep 6h
hacker        73       0  0 12:15 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        90      73  0 12:15 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/31489-run-10938
Yahaha, you found me! Here is your flag:
pwn.college{QG7CO_EakxdBM4Ia-DYpM9rbCMW.dhzM4QDLzkTN0czW}
```
# Killing Processes-

To kill a processes working in the terminal we have to first find the processes PID then use kill command with argument of PID of the process we have to end.For this challenge we have to first find the PID of /challenge/dont_run and kill it then run /challenge/run.

```bash
Connected!
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  1 12:19 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /ru
root           7       1  0 12:19 ?        00:00:00 /run/dojo/bin/sleep 6h
root          71       1  0 12:19 ?        00:00:00 su -c /challenge/.launcher hacker
hacker        73      71  0 12:19 ?        00:00:00 /challenge/dont_run
hacker        74      73  0 12:19 ?        00:00:00 sleep 6h
hacker        75       0  1 12:19 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        92      75  0 12:19 pts/0    00:00:00 ps -ef
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{4qZr7esN7MPzB1kKkoc2alF85BI.dJDN4QDLzkTN0czW}
```
# interrupting Processes-

We can interrupt the processes clogging the terminal by ctrl+c. this will interupt any process waiting for the input.In this challenge, we have to run /challenge/run and it will wait for the input, then we will interupt it using ctrl+c.

```bash
Connected!
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{05YJO9LdmLX9VD6eiUdnmNqDrkB.dNDN4QDLzkTN0czW}
```
# Suspending Processes-

We can suspend or stop a processes working in terminal by ctrl + Z.For this challenge, we have to first run /challenge/run which requires a copy of it running in terminal before it gives the flag so we suspend a copy of /challenge/run.

```bash
Connected!
hacker@processes~suspending-processes:~$ run
ssh-entrypoint: run: command not found
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          83      65  0 12:30 pts/0    00:00:00 bash /challenge/run
root          85      83  0 12:30 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          83      65  0 12:30 pts/0    00:00:00 bash /challenge/run
root          90      65  0 12:30 pts/0    00:00:00 bash /challenge/run
root          92      90  0 12:30 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{USWPt8MA1ye5IIRoKKhJlLzEaNg.dVDN4QDLzkTN0czW}

```
# Resuming Processes-

we resume a suspended processes by fg the command.For this challenge we have first suspend /challenge/run then resume it to get the flag.

```bash
Connected!
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg /challenge/run
/challenge/run
I'm back! Here's your flag:
pwn.college{giDRNoqjZDfski9By-53IXM6LD7.dZDN4QDLzkTN0czW}
Don't forget to press Enter to quit me!

Goodbye!
```
# Backgrounding Processes-

We put a suspended a process into background by bg command. For this challenge, we have to first suspend /challenge/run then we bg the /challenge/run then pass it again as /challenge/run.

```bash
Connected!
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{o4YMyHCscBtSruUoKTXXPY0VKbL.ddDN4QDLzkTN0czW}
```
# Foregrounding Processes-

we can foreground a background process by fg it. for this challenge like previous challenge we have to first bg /challenge/run then fg it to get the flag.
.
```bash
Connected!
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
hacker@processes~foregrounding-processes:~$ fg /challenge/run
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{cMkrzu4L0FFwRvEsHGn60l599PR.dhDN4QDLzkTN0czW}
```
# Starting background processes-

We can start a command in background from the start by giving it argument of & and run it.For this challenge, we have to start /challenge/run in background 

```bash
Connected!
hacker@processes~starting-backgrounded-processes:~$ /challenge/run a
You've started me in the foreground! You must start me in the background (by
appending '&' to the command) to get the flag!
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 85



hacker@processes~starting-backgrounded-processes:~$ Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{o9PZ7cAlRp0WfJycuH0A_Wg9EbD.dlDN4QDLzkTN0czW}

[1]+  Done                    /challenge/run
```
# Process Exit Codes-

When a command is executed they get terminated with a exit code which can fetched by echo with the argument $?. For this challenge, we first run /challenge/get-code which gives a error code which we have to get by $? then pass it as argument to /challenge/submit-code.

```bash
Connected!
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
100
hacker@processes~process-exit-codes:~$ /challenge/submit-code 100
CORRECT! Here is your flag:
pwn.college{UmRmpmXA7V07SpV1KFh_AC47chn.dljN4UDLzkTN0czW}
```
