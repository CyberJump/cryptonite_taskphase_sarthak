
# Digesting Documentation

# Learning from documentation-
 
For this challenge, we have to use /challenge/challenge command with an argument --giveflag which will inturn give the required flag that we need for this challenge.

```bash
Connected!
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{keoAd0bprMs1X0GTJ3FHMadjBO9.dRjM5QDLzkTN0czW}
```
# Learning Complex Usage-
 
Many commands have arguments for their arguments. we will use this property to complete this challenge. we will use --printfile argument of /challenge/challenge with argument of /flag.

```bash
Connected!
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{8p5sZfb-ONIOpoHTShWODZ_AMSl.dVjM5QDLzkTN0czW}
```
# Reading Manuals-
 
we use the command man for manual which takes command as argument and gives out all the information about the command.For this challenge, we man challenge command which gives all information about the command challenge. Upon reading this manual,we observe that the argument --zwlchb with argument 284 will give the flag.

```bash
Connected!
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                                            Challenge Commands                                           CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --zwlchb NUM
              print the flag if NUM is 284

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                  May 2024                                                CHALLENGE(1)
hacker@man~reading-manuals:~$ /challenge/challenge --zwlchb 284
Correct usage! Your flag: pwn.college{YVLJC2-VFI8NZYzYwlchCA_bcpp.dRTM4QDLzkTN0czW}
```
# Searching Manuals-
 
we can search a manual by / and using n to go to next result.For this challenge we will man challenge then /flag to find all instances of flag being called in the manual.upon reading the different result we will get an argument --yhyup which will give the flag.

```bash
Connected!
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --yhyup
Initializing...
Correct usage! Your flag: pwn.college{cFiaX0ndMXOLvk7_kfKWQiHmWCi.dVTM4QDLzkTN0czW}
```
# Searching Manuals-
 
For this challenge we use man man which give the manual for manual function. Upon reading the manual carefully we find an argument of man -k which finds manuals containg required term with the short description about the function.In this we will find a command named givzhvoelh which will print flag. so upon man this command we will open the /challenge/challenge manual and we will find that an argument --givzhv with 464 will print the required flag for this challenge.

```bash
hacker@man~searching-for-manuals:~$ man man
MAN(1)                                                  Manual pager utils                                                 MAN(1)

NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man is the system's manual pager.  Each page argument given to man is normally the name of a program, utility or function.
       The manual page associated with each of these arguments is then found and displayed.  A section, if provided, will  direct
       man  to look only in that section of the manual.  The default action is to search in all of the available sections follow‐
       ing a pre-defined order (see DEFAULTS), and to show only the first page found, even if page exists in several sections.

       The table below shows the section numbers of the manual followed by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions, e.g. /etc/passwd
       6   Games
       7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7)
       8   System administration commands (usually only for root)
       9   Kernel routines [Non standard]

       A manual page consists of several sections.
hacker@man~searching-for-manuals:~$ man -k flag
dpkg-buildflags (1)  - returns build flags to use during package build
Dpkg::BuildFlags (3perl) - query build flags
fegetexceptflag (3)  - floating-point rounding and exception handling
fesetexceptflag (3)  - floating-point rounding and exception handling
givzhvoelh (1)       - print the flag!
i386 (8)             - change reported architecture in new program environment and/or set personality flags
ioctl_iflags (2)     - ioctl() operations for inode flags
linux32 (1)          - change reported architecture in new program environment and/or set personality flags
linux64 (1)          - change reported architecture in new program environment and/or set personality flags
pcap-config (1)      - write libpcap compiler and linker flags to standard output
security_compute_av_flags (3) - query the SELinux policy database in the kernel
security_compute_av_flags_raw (3) - query the SELinux policy database in the kernel
set_matchpathcon_flags (3) - set flags controlling the operation of matchpathcon or matchpathcon_index and configure the behaviour...
set_matchpathcon_invalidcon (3) - set flags controlling the operation of matchpathcon or matchpathcon_index and configure the beha...
set_matchpathcon_printf (3) - set flags controlling the operation of matchpathcon or matchpathcon_index and configure the behaviou...
setarch (1)          - change reported architecture in new program environment and/or set personality flags
setarch (8)          - change reported architecture in new program environment and/or set personality flags
x86_64 (8)           - change reported architecture in new program environment and/or set personality flags
hacker@man~searching-for-manuals:~$ man givzhvoelh

CHALLENGE(1)                                            Challenge Commands                                           CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --givzhv NUM
              print the flag if NUM is 464

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                  May 2024                                                CHALLENGE(1)
hacker@man~searching-for-manuals:~$ /challenge/challenge --givzhv 464
Correct usage! Your flag: pwn.college{giv_Hzh4v6Hoel4hhgJ-LHKIGwR.dZTM4QDLzkTN0czW}
```
# Helpful Programs-
 
some programs use --help to give info about them.For this challenge we use --help on /challenge/challenge which give helpful arguments for this command. we first use -p argument to get the value 248 which when passed with argument -g will print the flag.

```bash
Connected!
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 248
hacker@man~helpful-programs:~$ /challenge/challenge -g 248
Correct usage! Your flag: pwn.college{AHKmN_wLsitSZ2a4gY8L9OW9OYA.ddjM4QDLzkTN0czW}
```
# Help For builtins-
 
We use the help for inbuilt shell builtins.For this challenge, the command challenge is a shell builtin so we pass help with challenge as an argument.This gives the helpful arguments of challenge along with the secret value to get the flag. Now,passing the secret value with the argument --secret will give the flag.

```bash
Connected!
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "gGxnwJFc".
hacker@man~help-for-builtins:~$ challenge --secret gGxnwJFc
Correct! Here is your flag!
pwn.college{gGxnwJFczIOd5AzjeyBuFXea2X1.dRTM5QDLzkTN0czW}
```

