
# Comprehending Commands

# Cat : not the pet,but the command-

Cat is the command to read out the content of the arguement file. So, to get this challenge flag we just have to read out the file flag.

```bash
Connected!
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{QxENJ9F-83x_noqmFJFi_4j6kc-.dFzN1QDLzkTN0czW}
```

# Catting Absolute Paths-

To obtain this flag, we have to give the absolute path of /flag as an argument to the command cat and we will get the flag for this command.

```bash
Connected!
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{4Cb4sDDgpHD6XU6Q6AJkS3ql3iV.dlTM5QDLzkTN0czW}
```
# More Catting Practice-

For this challenge, changing directory is prohibited so we cant cd. so we will cat the flag while via its absolute path which is /usr/share/glib-2.0/flag which is given in the terminal when we start the challenge.

```bash
Connected!
You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/share/glib-2.0/flag. Go cat it out **without** cding into that
directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/glib-2.0/flag
pwn.college{4rVn8SF0UXRQe-MLRDeE_Q_ySng.dBjM5QDLzkTN0czW}
```
# Grepping for a needle in a haystack -

Grep is a command which searches for the required content from a large amount of data. In this challenege we are given with a file /challenge/data.txt, so we grep the file for a pwn.college because the flag starts with pwn.college.

```bash
Connected!
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{oKlWjXDAkeKZy33Murs14G1zTxo.ddTM4QDLzkTN0czW}
```
# Listing files-

In this challenge we have to use command ls which lists all the files present in the given directory.For this challenge, we are given that the /challenge contains flag while with a different name.So, we ls the /challenge directory and then we will be given the file flag with different name 22826-renamed-run-29392 after which we just give the command /challenge/22826-renamed-run-29392.

```bash
Connected!
hacker@commands~listing-files:~$ ls /challenge
22826-renamed-run-29392  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/22826-renamed-run-29392
Yahaha, you found me! Here is your flag:
pwn.college{Esdp65POYSSuXllIlyvveJ2EPRZ.dhjM4QDLzkTN0czW}
```
# Touching flies-

The touch command creates a new blank file. For this challenege,we have to first touch two files /tmp/pwn and /tmp/college. after touching these two files then we just execute the command /challenge/run command. This will give us the required flag for this challenge.

```bash
Connected!
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{gbP4fHgok4OFty1WgfYFfpRUM6b.dBzM4QDLzkTN0czW}
```
# Removing files-

To remove a file we pass the command rm with the argument of the file we have to delete.For this challenge, we have to first detele a given file delete_me by rm command. after which we pass the command /challenge/check which will give the required flag.

```bash
Connected!
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{AyjEBFtSA8KbE8tO1H4jBpVCzFw.dZTOwUDLzkTN0czW}
```
# Hidden files-

Some files can be hidden by just adding . before the file name which cant be easily found out by ls. So find such files we pass the ls command with a argument -a which will also list hidden files. For this challenge, we have to cd to directory / and then pass the command ls -a which will list out hidden files and we can observe that it contains a file .flag-1836302971123. Finally we just, cat the file.

```bash
Connected!
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv           bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-1836302971123  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-1836302971123
pwn.college{IOM9JGAdD3fpzpByrn_XSXXIWxr.dBTN4QDLzkTN0czW}
```
# An Epic File System Quest-

For this challenge, we have to make use of cat,ls and ls -a to find the files with clues in different directories. So for the first clue we ls the directory / to find the TEASER upon catting this file we will get the path to the directory for next clue which is /usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL. However we cant directly ls so we have to change the directory to this directory, then ls the directory which will get us the file SNIPPET and upon catting this file we will the directory for next clue. We will make use of ls and ls -a to list out the content of directories without having to cd to them will prevent self destructing files from destroying and also find hidden files after which we cat the files with its absolute path. This has to done multiple times until we reach the required file upon catting that file we get the needed flag.

```bash
Connected!
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
TEASER  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin     challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat TEASER
Tubular find!
The next clue is in: /usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls
SNIPPET  Y.pl
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat SNIPPET
Yahaha, you found me!
The next clue is in: /usr/share/racket/pkgs/gui-lib/hierlist/compiled
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls /usr/share/racket/pkgs/gui-lib/hierlist/compiled
NOTE  hierlist_rkt.dep  hierlist_rkt.zo
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /usr/share/racket/pkgs/gui-lib/hierlist/compiled/NOTE
Great sleuthing!
The next clue is in: /usr/share/doc/qemu-system-x86

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls -a /usr/share/doc/qemu-system-x86
.  ..  .DISPATCH  NEWS.Debian.gz  README.Debian  changelog.Debian.gz  common  copyright
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /usr/share/doc/qemu-system-x86/.DISPATCH
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/pip/_internal/vcs

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls /usr/local/lib/python3.8/dist-packages/pip/_internal/vcs
LEAD-TRAPPED  __init__.py  __pycache__  bazaar.py  git.py  mercurial.py  subversion.py  versioncontrol.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /usr/local/lib/python3.8/dist-packages/pip/_internal/vcs/LEAD-TRAPPED
Tubular find!
The next clue is in: /opt/linux/linux-5.4/block/partitions

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls -a /opt/linux/linux-5.4/block/partitions
.                .efi.o.cmd    acorn.h  atari.c     check.o    efi.o    ldm.c    msdos.h  sgi.h     ultrix.c
..               .msdos.o.cmd  aix.c    atari.h     cmdline.c  ibm.c    ldm.h    msdos.o  sun.c     ultrix.h
.CUE             Kconfig       aix.h    built-in.a  cmdline.h  ibm.h    mac.c    osf.c    sun.h
.built-in.a.cmd  Makefile      amiga.c  check.c     efi.c      karma.c  mac.h    osf.h    sysv68.c
.check.o.cmd     acorn.c       amiga.h  check.h     efi.h      karma.h  msdos.c  sgi.c    sysv68.h
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /opt/linux/linux-5.4/block/partitions/.CUE
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/include/config/arch/has/set/direct

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls /opt/linux/linux-5.4/include/config/arch/has/set/direct
INFO-TRAPPED  map.h
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /opt/linux/linux-5.4/include/config/arch/has/set/direct/INFO-TRAPPED
Yahaha, you found me!
The next clue is in: /usr/share/racket/pkgs/srfi-lib/srfi/48/compiled
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls /usr/share/racket/pkgs/srfi-lib/srfi/48/compiled
TIP  format_rkt.dep  format_rkt.zo
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /usr/share/racket/pkgs/srfi-lib/srfi/48/compiled/TIP
Tubular find!
The next clue is in: /opt/aflplusplus/nyx_mode/QEMU-Nyx/include/hw/tricore

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ ls /opt/aflplusplus/nyx_mode/QEMU-Nyx/include/hw/tricore
NUGGET-TRAPPED  tricore.h
hacker@commands~an-epic-filesystem-quest:/usr/lib/x86_64-linux-gnu/perl-base/unicore/lib/CWL$ cat /opt/aflplusplus/nyx_mode/QEMU-Nyx/include/hw/tricore/NUGGET-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{AX18mOOZPH3-AsxSuyG8rIOrZqb.dljM4QDLzkTN0czW}
```
# Making Directories-

we can create directories by making use of command mkdir. For this challenge we have make directory /tmp/pwn and cd to this directory. After which we make a file college by touch command and pass the command /challenge/run to get the required flag.
```bash
Connected!
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{sVYtuoH7r2J16UAGMXHWAe8e22R.dFzM4QDLzkTN0czW}
```

# Finding files-

Find command is used to find a particular file or number of files matching the given criteria.For this challenge, we utilize this command to get all files named flag in the filesystem by the command find / -name flag. This will list out a lot of number of files, so we cat the files and by trial and error we get the file containing the required flag to complete this challenge.
```bash
Connected!
hacker@commands~finding-files:~$ find / -name flag
find: ‘/tmp/tmp.MiOQGWw5Zc’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
/usr/share/racket/pkgs/sasl-doc/compiled/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/root’: Permission denied
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/local/share/radare2/5.9.5/flag
cat: /usr/local/share/radare2/5.9.5/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/share/racket/pkgs/sasl-doc/compiled/flag
pwn.college{c9FXzE-U2oGPFEHeuW3eXhbjENm.dJzM4QDLzkTN0czW}
```
# Linking Files-

We use a soft/symbolic link, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file. By this property, we try to make a symbolic link of /flag file with /home/hacker/not-the-flag.so when we pass the command /challenge/catflag it will read out the contents of file /home/hacker/not-the-flag which a symbolic link to /flag which in turn gives us the required flag to complete this challenge.
```bash
Connected!
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{QM-qoNRchovsNf3006rrXceEMvt.dlTM1UDLzkTN0czW}
```

