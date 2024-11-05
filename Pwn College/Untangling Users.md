
# Untangling Users -

# Becoming root with su-

you can change the user access by su command but this requires a root password for authentication. for this challenge, we have to use su with the password hack-the-planet and cat /flag file.

```bash
Connected!
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{M7FmINutwDzdO_RymLzb_izWaWS.dVTN0UDLzkTN0czW}
```
# Other users with su-

we can also change the user by su command by giving the username as argument and password of username. For this challenge, we have to first get zardus login then run /challenge/run.

```bash
Connected!
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{guL2JhFI08MgX1MKEDVGdnL2ywh.dZTN0UDLzkTN0czW}
```
# Cracking Passwords-

Usually the passwords are hashed and stored in files which are protected by root access however sometimes leaks also occur which can unhashed by john the ripper command. For this challenge we first john /challenge/shadow-leak to get the password of zardus after which su zardus and run /challenge/run.

```bash
Connected!
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:03 40% 1/3 0g/s 308.6p/s 308.6c/s 308.6C/s .zardus99999..Mrzardus
0g 0:00:00:07 76% 1/3 0g/s 281.1p/s 281.1c/s 281.1C/s 9999945..Z9999932
0g 0:00:00:09 91% 1/3 0g/s 273.6p/s 273.6c/s 273.6C/s zardus999991978..zardus2002
0g 0:00:00:10 98% 1/3 0g/s 275.3p/s 275.3c/s 275.3C/s zardus999991939..zardus1915
0g 0:00:00:12 0% 2/3 0g/s 279.4p/s 279.4c/s 279.4C/s brenda..keith
0g 0:00:00:14 0% 2/3 0g/s 282.0p/s 282.0c/s 282.0C/s serena..88888888
0g 0:00:00:16 0% 2/3 0g/s 281.5p/s 281.5c/s 281.5C/s national..rocket1
0g 0:00:00:18 1% 2/3 0g/s 281.7p/s 281.7c/s 281.7C/s katrina..karla
0g 0:00:00:20 1% 2/3 0g/s 283.7p/s 283.7c/s 283.7C/s Johnson..buzz
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04878g/s 284.0p/s 284.0c/s 284.0C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{gsP4iti2UgArJ_Hz0tNZ_MUp46k.ddTN0UDLzkTN0czW}
```
# Using Sudo-

Unlike su where we have to give password to give commands as root user however you can run a single command as root by sudo. For this challenge, we have to sudo cat /flag to read the /flag file with root access. 

```bash
Connected!
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{A7G6Qz_J8dz0E4cbvsRcO8IiIXH.dhTN0UDLzkTN0czW}
```
