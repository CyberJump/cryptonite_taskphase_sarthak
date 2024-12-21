# Reverse Engineering

# 1) Bit-o-ASM 1

For this challenge we are given with an assembly dump and we have to find the value stored in eax 
![image](https://github.com/user-attachments/assets/e02f983c-1b53-47a0-a47c-138b37b3d371)

so i opened it up on notepad and slowly checked whats happening 
![image](https://github.com/user-attachments/assets/285229d6-13d3-4b8d-8d4c-d62158faf481)

so in this program the moved the value of edi to dword pointer and rsi into qword pointer and the eax with the value 0x30 which is 48 in decimal
```
Flag - picoCTF{48}

```

# 2) Bit-O-ASM 2

similar to the previous chall we are given with assembly dump and we have to find the value of eax

![image](https://github.com/user-attachments/assets/aaaad8ef-8ff5-4078-8d0c-2e3ee3c38211)

so here the value of rsp is moved to rbp, then DWORD ptr is moved with the value of edi, at <+15> dword pointer is moved with the value 0x9fe1a which is 654874 in decimal. this value is then pushed to eax.

```
FLAG- picoCTF{654874}

```
# 3) Vault Door 3

Alrighty then lets start with this challenge, so the nae is quite enticing as in looking for password. So the challenge starts with it a java program.

```
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        System.out.println(buffer);
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18gb41_u_4_mfr340");
    }
}
```

okk first of all the program is hugeeee and its in java. Lucky for me, I somewhat know java and i analysed the program.

So what i concurred was that so theres this function checkpassword which takes the password from the user and checks it with a jumbled up string. If it matches with the string. 

The way it jumbles up the true password is

1)It takes the letters from index 0-7 as it is\
2)It reverses the string from index 8-15\
3)For the last 16 letters what is does is\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-For even placed numbers,they would get reversed\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-For odd placed numbers,the letters would be taken as it is.

All right then now that we know this,Lets make a python program to reverse the effects
```
def find_password():
  target = "jU5t_a_sna_3lpm18gb41_u_4_mfr340"
  password = [""] * 32  

 
  for i in range(8):
      password[i] = target[i]

  
  for i in range(8, 16):
      password[i] = target[23 - i]


  for i in range(16, 32):
      if i % 2 == 0:
          password[i] = target[46 - i]
      else:
          password[i] = target[i]

  return "".join(password)
  
print(find_password())
```
well when i ran the program i got a output that was-
```
 jU5t_a_s1mpl3_an4gr4m_4_u_1fb380
```
I tried it and well it was wrong, Then i was stuck so took the hint which was to map ever value of buffer.so thats what i did.
```
password[0] = buffer[0] = 'j'
password[1] = buffer[1] = 'U'
password[2] = buffer[2] = '5'
password[3] = buffer[3] = 't'
password[4] = buffer[4] = '_'
password[5] = buffer[5] = 'a'
password[6] = buffer[6] = '_'
password[7] = buffer[7] = 's'
password[15] = buffer[8] = 'n'
password[14] = buffer[9] = 'a'
password[13] = buffer[10] = '_'
password[12] = buffer[11] = '3'
password[11] = buffer[12] = 'l'
password[10] = buffer[13] = 'p'
password[9] = buffer[14] = 'm'
password[8] = buffer[15] = '1'
password[30] = buffer[16] = '8'
password[28] = buffer[18] = '9'
password[26] = buffer[20] = '7'
password[24] = buffer[22] = '_'
password[22] = buffer[24] = '_'
password[20] = buffer[26] = 'm'
password[18] = buffer[28] = 'r'
password[16] = buffer[30] = '4'
password[31] = buffer[31] = 'f'
password[29] = buffer[29] = '5'
password[27] = buffer[27] = '9'
password[25] = buffer[25] = '4'
password[23] = buffer[23] = 'u'
password[21] = buffer[21] = '4'
password[19] = buffer[19] = 'g'
password[17] = buffer[17] = 'g'
```

Well then i tried to just to find the password by good old human trial and error. I can confirm that Paper and pencil is enough to solve anything and thats what i did .

the flag was

```
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}

```

VOILLAAAAA !!!!

# 4) GDB Baby step 1

All right so the challenge begins with it providing me with a file called debugger0_a and I have to find the value of eax.

![Screenshot_2024-12-21_16_35_12](https://github.com/user-attachments/assets/5c252570-ea8d-436f-92ef-ed3b3fcf33e1)

Ook then I opened up the first hint and it says use gdb debugger.

I searched up google about GDB the results which i got-

A debugger is a tool that helps you in this debugging process. It allows you to control the execution of your program, inspect its state at any point, and change its state if necessary. In other words, a debugger gives you the superpower to manipulate time (at least, for your program)

One of the key features of a debugger is the ability to set ‘breakpoints’. A breakpoint is a point in your code where the debugger will pause the execution of your program. This allows you to inspect the state of your program at that specific point, which can be incredibly useful for tracking down bugs.

and GDB is command used to call up GNU debugger.

so i started with installing gdb command
```
(kali㉿kali)-[~]
└─$ wget https://artifacts.picoctf.net/c/512/debugger0_a
--2024-12-21 11:59:51--  https://artifacts.picoctf.net/c/512/debugger0_a
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.159.61.26, 108.159.61.105, 108.159.61.96, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.159.61.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16472 (16K) [application/octet-stream]
Saving to: ‘debugger0_a’

debugger0_a               100%[==================================>]  16.09K  --.-KB/s    in 0s      

2024-12-21 11:59:57 (78.4 MB/s) - ‘debugger0_a’ saved [16472/16472]

                                                                                                     
┌──(kali㉿kali)-[~]
└─$ cd ./Downloads
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ GDB debugger0_a
GDB: command not found
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ sudo apt install GBD   
[sudo] password for kali: 
Error: Unable to locate package GBD
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ GDB            
GDB: command not found
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ sudo apt install GDB
Error: Unable to locate package GDB
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ gdb debugger0_a
Command 'gdb' not found, but can be installed with:
sudo apt install gdb        
sudo apt install gdb-minimal
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ sudo apt install gdb   
The following packages were automatically installed and are no longer required:
  ibverbs-providers         libgfrpc0          librados2        python3.11-minimal
  libboost-iostreams1.83.0  libgfxdr0          librdmacm1t64    samba-vfs-modules
  libboost-thread1.83.0     libglusterfs0      python3-lib2to3
  libcephfs2                libibverbs1        python3.11
  libgfapi0                 libpython3.11-dev  python3.11-dev
Use 'sudo apt autoremove' to remove them.

Installing:
  gdb
                                                                                                     
Installing dependencies:
  libbabeltrace1  libdebuginfod-common  libipt2                     libsource-highlight4t64
  libc6-dbg       libdebuginfod1t64     libsource-highlight-common                                   
                                                                                                     
Suggested packages:
  gdb-doc  gdbserver

Summary:
  Upgrading: 0, Installing: 8, Removing: 0, Not Upgrading: 1462
  Download size: 12.2 MB
  Space needed: 26.1 MB / 4418 MB available

Continue? [Y/n] y
Get:2 http://http.kali.org/kali kali-rolling/main amd64 libbabeltrace1 amd64 1.5.11-4+b1 [176 kB]
Get:1 http://mirrors.neusoft.edu.cn/kali kali-rolling/main amd64 libdebuginfod-common all 0.192-4 [23.7 kB]
Get:3 http://kali.download/kali kali-rolling/main amd64 libdebuginfod1t64 amd64 0.192-4 [32.4 kB]   
Get:4 http://kali.download/kali kali-rolling/main amd64 libipt2 amd64 2.1.1-1 [47.8 kB]             
Get:5 http://kali.download/kali kali-rolling/main amd64 libsource-highlight-common all 3.1.9-4.3 [77.5 kB]
Get:6 http://http.kali.org/kali kali-rolling/main amd64 libsource-highlight4t64 amd64 3.1.9-4.3+b1 [335 kB]
Get:7 http://mirror.freedif.org/kali kali-rolling/main amd64 gdb amd64 15.2-1 [4380 kB]             
Get:8 http://mirrors.neusoft.edu.cn/kali kali-rolling/main amd64 libc6-dbg amd64 2.40-3 [7097 kB] 
Fetched 12.2 MB in 1min 9s (177 kB/s)                                                               
Preconfiguring packages ...
Selecting previously unselected package libdebuginfod-common.
(Reading database ... 404534 files and directories currently installed.)
Preparing to unpack .../0-libdebuginfod-common_0.192-4_all.deb ...
Unpacking libdebuginfod-common (0.192-4) ...
Selecting previously unselected package libbabeltrace1:amd64.
Preparing to unpack .../1-libbabeltrace1_1.5.11-4+b1_amd64.deb ...
Unpacking libbabeltrace1:amd64 (1.5.11-4+b1) ...
Selecting previously unselected package libdebuginfod1t64:amd64.
Preparing to unpack .../2-libdebuginfod1t64_0.192-4_amd64.deb ...
Unpacking libdebuginfod1t64:amd64 (0.192-4) ...
Selecting previously unselected package libipt2.
Preparing to unpack .../3-libipt2_2.1.1-1_amd64.deb ...
Unpacking libipt2 (2.1.1-1) ...
Selecting previously unselected package libsource-highlight-common.
Preparing to unpack .../4-libsource-highlight-common_3.1.9-4.3_all.deb ...
Unpacking libsource-highlight-common (3.1.9-4.3) ...
Selecting previously unselected package libsource-highlight4t64:amd64.
Preparing to unpack .../5-libsource-highlight4t64_3.1.9-4.3+b1_amd64.deb ...
Unpacking libsource-highlight4t64:amd64 (3.1.9-4.3+b1) ...
Selecting previously unselected package gdb.
Preparing to unpack .../6-gdb_15.2-1_amd64.deb ...
Unpacking gdb (15.2-1) ...
Selecting previously unselected package libc6-dbg:amd64.
Preparing to unpack .../7-libc6-dbg_2.40-3_amd64.deb ...
Unpacking libc6-dbg:amd64 (2.40-3) ...
Setting up libdebuginfod-common (0.192-4) ...
Setting up libsource-highlight-common (3.1.9-4.3) ...
Setting up libc6-dbg:amd64 (2.40-3) ...
Setting up libipt2 (2.1.1-1) ...
Setting up libbabeltrace1:amd64 (1.5.11-4+b1) ...
Setting up libdebuginfod1t64:amd64 (0.192-4) ...
Setting up libsource-highlight4t64:amd64 (3.1.9-4.3+b1) ...
Setting up gdb (15.2-1) ...
Processing triggers for libc-bin (2.40-3) ...
Processing triggers for man-db (2.12.1-2) ...
Processing triggers for kali-menu (2024.3.1) ...
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ sudo apt install gdb-minimal
The following packages were automatically installed and are no longer required:
  ibverbs-providers         libgfapi0          librados2                   python3.11-dev
  libbabeltrace1            libgfrpc0          librdmacm1t64               python3.11-minimal
  libboost-iostreams1.83.0  libgfxdr0          libsource-highlight-common  samba-vfs-modules
  libboost-thread1.83.0     libglusterfs0      libsource-highlight4t64
  libc6-dbg                 libibverbs1        python3-lib2to3
  libcephfs2                libpython3.11-dev  python3.11
Use 'sudo apt autoremove' to remove them.

Installing:
  gdb-minimal
                                                                                                     
REMOVING:
  gdb
                                                                                                     
Summary:
  Upgrading: 0, Installing: 1, Removing: 1, Not Upgrading: 1462
  Download size: 3546 kB
  Freed space: 2173 kB

Continue? [Y/n] n
Abort.
                                                                                                     
┌──(kali㉿kali)-[~/Downloads]
└─$ gdb debugger0_a 
GNU gdb (Debian 15.2-1) 15.2
Copyright (C) 2024 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) help
List of classes of commands:

aliases -- User-defined aliases of other commands.
breakpoints -- Making program stop at certain points.
data -- Examining data.
files -- Specifying and examining files.
internals -- Maintenance commands.
obscure -- Obscure features.
running -- Running the program.
stack -- Examining the stack.
status -- Status inquiries.
support -- Support facilities.
text-user-interface -- TUI is the GDB text based interface.
tracepoints -- Tracing of program execution without stopping the program.
user-defined -- User-defined commands.

Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) fjf
Undefined command: "fjf".  Try "help".                                                                                                                                                                                                      
(gdb) exit
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/Downloads]
└─$ file debugger0_a  
debugger0_a: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=15a10290db2cd2ec0c123cf80b88ed7d7f5cf9ff, for GNU/Linux 3.2.0, not stripped
                                                                                                      
┌──(kali㉿kali)-[~/Downloads]
└─$ gdb debugger0_a 
GNU gdb (Debian 15.2-1) 15.2
Copyright (C) 2024 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) hel
List of classes of commands:

aliases -- User-defined aliases of other commands.
breakpoints -- Making program stop at certain points.
data -- Examining data.
files -- Specifying and examining files.
internals -- Maintenance commands.
obscure -- Obscure features.
running -- Running the program.
stack -- Examining the stack.
status -- Status inquiries.
support -- Support facilities.
text-user-interface -- TUI is the GDB text based interface.
tracepoints -- Tracing of program execution without stopping the program.
user-defined -- User-defined commands.

Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) help
List of classes of commands:

aliases -- User-defined aliases of other commands.
breakpoints -- Making program stop at certain points.
data -- Examining data.
files -- Specifying and examining files.
internals -- Maintenance commands.
obscure -- Obscure features.
running -- Running the program.
stack -- Examining the stack.
status -- Status inquiries.
support -- Support facilities.
text-user-interface -- TUI is the GDB text based interface.
tracepoints -- Tracing of program execution without stopping the program.
user-defined -- User-defined commands.

Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) data
Undefined command: "data".  Try "help".
(gdb) help data
Examining data.

List of commands:

agent-printf -- Target agent only formatted printing, like the C "printf" function.
append -- Append target code/data to a local file.
append binary -- Append target code/data to a raw binary file.
append binary memory -- Append contents of memory to a raw binary file.
append binary value -- Append the value of an expression to a raw binary file.
append memory -- Append contents of memory to a raw binary file.
append value -- Append the value of an expression to a raw binary file.
call -- Call a function in the program.
disassemble -- Disassemble a specified section of memory.
display -- Print value of expression EXP each time the program stops.
dump -- Dump target code/data to a local file.
dump binary -- Write target code/data to a raw binary file.
dump binary memory -- Write contents of memory to a raw binary file.
dump binary value -- Write the value of an expression to a raw binary file.
dump ihex -- Write target code/data to an intel hex file.
dump ihex memory -- Write contents of memory to an ihex file.
dump ihex value -- Write the value of an expression to an ihex file.
dump memory -- Write contents of memory to a raw binary file.
dump srec -- Write target code/data to an srec file.
dump srec memory -- Write contents of memory to an srec file.
dump srec value -- Write the value of an expression to an srec file.
dump tekhex -- Write target code/data to a tekhex file.
dump tekhex memory -- Write contents of memory to a tekhex file.
dump tekhex value -- Write the value of an expression to a tekhex file.
dump value -- Write the value of an expression to a raw binary file.
dump verilog -- Write target code/data to a verilog hex file.
dump verilog memory -- Write contents of memory to a verilog hex file.
dump verilog value -- Write the value of an expression to a verilog hex file.
explore -- Explore a value or a type valid in the current context.
explore type -- Explore a type or the type of an expression.
explore value -- Explore value of an expression valid in the current context.
find -- Search memory for a sequence of bytes.
init-if-undefined -- Initialize a convenience variable if necessary.
mem -- Define attributes for memory region or reset memory region handling to target-based.
memory-tag -- Generic command for printing and manipulating memory tag properties.
memory-tag check -- Validate a pointer's logical tag against the allocation tag.
memory-tag print-allocation-tag -- Print the allocation tag for ADDRESS.
memory-tag print-logical-tag -- Print the logical tag from POINTER.
memory-tag set-allocation-tag -- Set the allocation tag(s) for a memory range.
memory-tag with-logical-tag -- Print a POINTER with a specific logical TAG.
output -- Like "print" but don't put in value history and don't print newline.
print, inspect, p -- Print value of expression EXP.
print-object, po -- Ask an Objective-C object to print itself.
printf -- Formatted printing, like the C "printf" function.
ptype -- Print definition of type TYPE.
restore -- Restore the contents of FILE to target memory.
set -- Evaluate expression EXP and assign result to variable VAR.
set ada -- Prefix command for changing Ada-specific settings.
set ada print-signatures -- Enable or disable the output of formal and return types for functions in the overloads selection menu.
set ada source-charset -- Set the Ada source character set.
set ada trust-PAD-over-XVS -- Enable or disable an optimization trusting PAD types over XVS types.
set agent -- Set debugger's willingness to use agent as a helper.
set always-read-ctf -- Set whether CTF is always read.
--Type <RET> for more, q to quit, c to continue without paging--
set annotate -- Set annotation_level.
set architecture, set processor -- Set architecture of target.
set args -- Set argument list to give program being debugged when it is started.
set auto-connect-native-target -- Set whether GDB may automatically connect to the native target.
set auto-load -- Auto-loading specific settings.
set auto-load gdb-scripts -- Enable or disable auto-loading of canned sequences of commands scripts.
set auto-load libthread-db -- Enable or disable auto-loading of inferior specific libthread_db.
set auto-load local-gdbinit -- Enable or disable auto-loading of .gdbinit script in current directory.
set auto-load python-scripts -- Set the debugger's behaviour regarding auto-loaded Python scripts.
set auto-load safe-path -- Set the list of files and directories that are safe for auto-loading.
set auto-load scripts-directory -- Set the list of directories from which to load auto-loaded scripts.
set auto-solib-add -- Set autoloading of shared library symbols.
set backtrace -- Set backtrace specific variables.
set backtrace limit -- Set an upper bound on the number of backtrace levels.
set backtrace past-entry -- Set whether backtraces should continue past the entry point of a program.
set backtrace past-main -- Set whether backtraces should continue past "main".
set basenames-may-differ -- Set whether a source file may have multiple base names.
set breakpoint -- Breakpoint specific settings.
set breakpoint always-inserted -- Set mode for inserting breakpoints.
set breakpoint auto-hw -- Set automatic usage of hardware breakpoints.
set breakpoint condition-evaluation -- Set mode of breakpoint condition evaluation.
set breakpoint pending -- Set debugger's behavior regarding pending breakpoints.
set can-use-hw-watchpoints -- Set debugger's willingness to use watchpoint hardware.
set case-sensitive -- Set case sensitivity in name search (on/off/auto).
set charset -- Set the host and target character sets.
set check, set ch, set c -- Set the status of the type/range checker.
set check range -- Set range checking (on/warn/off/auto).
set check type -- Set strict type checking.
set circular-trace-buffer -- Set target's use of circular trace buffer.
set code-cache -- Set cache use for code segment access.
set coerce-float-to-double -- Set coercion of floats to doubles when calling functions.
set compile-args -- Set compile command GCC command-line arguments.
set compile-gcc -- Set compile command GCC driver filename.
set complaints -- Set max number of complaints about incorrect symbols.
set confirm -- Set whether to confirm potentially dangerous operations.
set cp-abi -- Set the ABI used for inspecting C++ objects.
set cwd -- Set the current working directory to be used when the inferior is started.
set data-directory -- Set GDB's data directory.
set dcache -- Use this command to set number of lines in dcache and line-size.
set dcache line-size -- Set dcache line size in bytes (must be power of 2).
set dcache size -- Set number of dcache lines.
set debug -- Generic command for setting gdb debugging flags.
set debug arch -- Set architecture debugging.
set debug auto-load -- Set auto-load verifications debugging.
set debug bfd-cache -- Set bfd cache debugging.
set debug breakpoint -- Set breakpoint location debugging.
set debug check-physname -- Set cross-checking of "physname" code against demangler.
set debug coff-pe-read -- Set coff PE read debugging.
set debug compile -- Set compile command debugging.
set debug compile-cplus-scopes -- Set debugging of C++ compile scopes.
set debug compile-cplus-types -- Set debugging of C++ compile type conversion.
set debug displaced -- Set displaced stepping debugging.
set debug dwarf-die -- Set debugging of the DWARF DIE reader.
set debug dwarf-line -- Set debugging of the dwarf line reader.
set debug dwarf-read -- Set debugging of the DWARF reader.
set debug entry-values -- Set entry values and tail call frames debugging.
--Type <RET> for more, q to quit, c to continue without paging--
set debug event-loop -- Set event-loop debugging.
set debug expression -- Set expression debugging.
set debug fortran-array-slicing -- Set debugging of Fortran array slicing.
set debug frame -- Set frame debugging.
set debug index-cache -- Set display of index-cache debug messages.
set debug infcall -- Set inferior call debugging.
set debug infrun -- Set inferior debugging.
set debug jit -- Set JIT debugging.
set debug libthread-db -- Set libthread-db debugging.
set debug linux-namespaces -- Set debugging of GNU/Linux namespaces module.
set debug linux-nat -- Set debugging of GNU/Linux native target.
set debug notification -- Set debugging of async remote notification.
set debug observer -- Set observer debugging.
set debug overload -- Set debugging of C++ overloading.
set debug parser -- Set parser debugging.
set debug py-breakpoint -- Set Python breakpoint debugging.
set debug py-micmd -- Set Python micmd debugging.
set debug py-unwind -- Set Python unwinder debugging.
set debug record -- Set debugging of record/replay feature.
set debug remote -- Set debugging of remote protocol.
set debug remote-packet-max-chars -- Set the maximum number of characters to display for each remote packet.
set debug separate-debug-file -- Set printing of separate debug info file search debug.
set debug serial -- Set serial debugging.
set debug skip -- Set whether to print the debug output about skipping files and functions.
set debug solib -- Set solib debugging.
set debug stap-expression -- Set SystemTap expression debugging.
set debug symbol-lookup -- Set debugging of symbol lookup.
set debug symfile -- Set debugging of the symfile functions.
set debug symtab-create -- Set debugging of symbol table creation.
set debug target -- Set target debugging.
set debug threads -- Set thread debugging.
set debug timestamp -- Set timestamping of debugging messages.
set debug tui -- Set tui debugging.
set debug varobj -- Set varobj debugging.
set debug xml -- Set XML parser debugging.
set debug-file-directory -- Set the directories where separate debug symbols are searched for.
set debuginfod -- Set debuginfod options.
set debuginfod enabled -- Set whether to use debuginfod.
set debuginfod urls -- Set the list of debuginfod server URLs.
set debuginfod verbose -- Set verbosity of debuginfod output.
set default-collect -- Set the list of expressions to collect by default.
set demangle-style -- Set the current C++ demangling style.
set detach-on-fork -- Set whether gdb will detach the child of a fork.
set direct-call-timeout -- Set the timeout, for direct calls to inferior function calls.
set directories -- Set the search path for finding source files.
set disable-randomization -- Set disabling of debuggee's virtual address space randomization.
set disassemble-next-line -- Set whether to disassemble next source line or insn when execution stops.
set disassembler-options -- Set the disassembler options.
set disassembly-flavor -- Set the disassembly flavor.
set disconnected-dprintf -- Set whether dprintf continues after GDB disconnects.
set disconnected-tracing -- Set whether tracing continues after GDB disconnects.
set displaced-stepping -- Set debugger's willingness to use displaced stepping.
set dprintf-channel -- Set the channel to use for dynamic printf.
set dprintf-function -- Set the function to use for dynamic printf.
set dprintf-style -- Set the style of usage for dynamic printf.
set dump-excluded-mappings -- Set whether gcore should dump mappings marked with the VM_DONTDUMP flag.--Type <RET> for more, q to quit, c to continue without paging--

set editing -- Set editing of command lines as they are typed.
set endian -- Set endianness of target.
set environment -- Set environment variable value to give the program.
set exec-direction -- Set direction of execution.
set exec-done-display -- Set notification of completion for asynchronous execution commands.
set exec-file-mismatch -- Set exec-file-mismatch handling (ask|warn|off).
set exec-wrapper -- Set a wrapper for running programs.
set extended-prompt -- Set the extended prompt.
set extension-language -- Set mapping between filename extension and source language.
set filename-display -- Set how to display filenames.
set follow-exec-mode -- Set debugger response to a program call of exec.
set follow-fork-mode -- Set debugger response to a program call of fork or vfork.
set fortran -- Prefix command for changing Fortran-specific settings.
set fortran repack-array-slices -- Enable or disable repacking of non-contiguous array slices.
set frame-filter -- Prefix command for 'set' frame-filter related operations.
set frame-filter priority -- GDB command to set the priority of the specified frame-filter.
set gnutarget, set g -- Set the current BFD target.
set guile, set gu -- Prefix command for Guile preference settings.
set guile print-stack -- Set mode for Guile exception printing on error.
set height -- Set number of lines in a page for GDB output pagination.
set history -- Generic command for setting command history parameters.
set history expansion -- Set history expansion on command input.
set history filename -- Set the filename in which to record the command history.
set history remove-duplicates -- Set how far back in history to look for and remove duplicate entries.
set history save -- Set saving of the history record on exit.
set history size -- Set the size of the command history.
set host-charset -- Set the host character set.
set index-cache -- Set index-cache options.
set index-cache directory -- Set the directory of the index cache.
set index-cache enabled -- Enable the index cache.
set indirect-call-timeout -- Set the timeout, for indirect calls to inferior function calls.
set inferior-tty, tty -- Set terminal for future runs of program being debugged.
set input-radix -- Set default input radix for entering numbers.
set interactive-mode -- Set whether GDB's standard input is a terminal.
set language -- Set the current source language.
set libthread-db-search-path -- Set search path for libthread_db.
set listsize -- Set number of source lines gdb will list by default.
set logging -- Set logging options.
set logging debugredirect -- Set the logging debug output mode.
set logging enabled -- Enable logging.
set logging file -- Set the current logfile.
set logging overwrite -- Set whether logging overwrites or appends to the log file.
set logging redirect -- Set the logging output mode.
set max-completions -- Set maximum number of completion candidates.
set max-user-call-depth -- Set the max call depth for non-python/scheme user-defined commands.
set max-value-size -- Set maximum sized value gdb will load from the inferior.
set may-call-functions -- Set permission to call functions in the program.
set may-insert-breakpoints -- Set permission to insert breakpoints in the target.
set may-insert-fast-tracepoints -- Set permission to insert fast tracepoints in the target.
set may-insert-tracepoints -- Set permission to insert tracepoints in the target.
set may-interrupt -- Set permission to interrupt or signal the target.
set may-write-memory -- Set permission to write into target memory.
set may-write-registers -- Set permission to write into registers.
set mem -- Memory regions settings.
set mem inaccessible-by-default -- Set handling of unknown memory regions.
set mi-async -- Set whether MI asynchronous mode is enabled.
--Type <RET> for more, q to quit, c to continue without paging--
set mpx -- Set Intel Memory Protection Extensions specific variables.
set multiple-symbols -- Set how the debugger handles ambiguities in expressions.
set non-stop -- Set whether gdb controls the inferior in non-stop mode.
set observer -- Set whether gdb controls the inferior in observer mode.
set opaque-type-resolution -- Set resolution of opaque struct/class/union types (if set before loading symbols).
set osabi -- Set OS ABI of target.
set output-radix -- Set default output radix for printing of values.
set overload-resolution -- Set overload resolution in evaluating C++ functions.
set pagination -- Set state of GDB output pagination.
set print, set pr, set p -- Generic command for setting how things print.
set print address -- Set printing of addresses.
set print array -- Set pretty formatting of arrays.
set print array-indexes -- Set printing of array indexes.
set print asm-demangle -- Set demangling of C++/ObjC names in disassembly listings.
set print characters -- Set limit on string chars to print.
set print demangle -- Set demangling of encoded C++/ObjC names when displaying symbols.
set print elements -- Set limit on array elements to print.
set print entry-values -- Set printing of function arguments at function entry.
set print finish -- Set whether `finish' prints the return value.
set print frame-arguments -- Set printing of non-scalar frame arguments.
set print frame-info -- Set printing of frame information.
set print inferior-events -- Set printing of inferior events (such as inferior start and exit).
set print max-depth -- Set maximum print depth for nested structures, unions and arrays.
set print max-symbolic-offset -- Set the largest offset that will be printed in <SYMBOL+1234> form.
set print memory-tag-violations -- Set printing of memory tag violations for pointers.
set print nibbles -- Set whether to print binary values in groups of four bits.
set print null-stop -- Set printing of char arrays to stop at first null char.
set print object -- Set printing of C++ virtual function tables.
set print pascal_static-members -- Set printing of pascal static members.
set print pretty -- Set pretty formatting of structures.
set print raw-frame-arguments -- Set whether to print frame arguments in raw form.
set print raw-values -- Set whether to print values in raw form.
set print repeats -- Set threshold for repeated print elements.
set print sevenbit-strings -- Set printing of 8-bit characters in strings as \nnn.
set print static-members -- Set printing of C++ static members.
set print symbol -- Set printing of symbol names when printing pointers.
set print symbol-filename -- Set printing of source filename and line number with <SYMBOL>.
set print symbol-loading -- Set printing of symbol loading messages.
set print thread-events -- Set printing of thread events (such as thread start and exit).
set print type -- Generic command for showing type-printing settings.
set print type hex -- Set printing of struct members sizes and offsets using hex notation.
set print type methods -- Set printing of methods defined in classes.
set print type nested-type-limit -- Set the number of recursive nested type definitions to print ("unlimited" or -1 to show all).
set print type typedefs -- Set printing of typedefs defined in classes.
set print union -- Set printing of unions interior to structures.
set print vtbl -- Set printing of C++ virtual function tables.
set prompt -- Set gdb's prompt.
set python -- Prefix command for python preference settings.
set python dont-write-bytecode -- Set whether the Python interpreter should avoid byte-compiling python modules.
set python ignore-environment -- Set whether the Python interpreter should ignore environment variables.
set python print-stack -- Set mode for Python stack dump on error.
set radix -- Set default input and output number radices.
set range-stepping -- Enable or disable range stepping.
set ravenscar -- Prefix command for changing Ravenscar-specific settings.
--Type <RET> for more, q to quit, c to continue without paging--
set ravenscar task-switching -- Enable or disable support for GNAT Ravenscar tasks.
set record, set rec -- Set record options.
set record btrace -- Set record options.
set record btrace bts -- Set record btrace bts options.
set record btrace bts buffer-size -- Set the record/replay bts buffer size.
set record btrace cpu -- Set the cpu to be used for trace decode.
set record btrace cpu auto -- Automatically determine the cpu to be used for trace decode.
set record btrace cpu none -- Do not enable errata workarounds for trace decode.
set record btrace pt -- Set record btrace pt options.
set record btrace pt buffer-size -- Set the record/replay pt buffer size.
set record btrace replay-memory-access -- Set what memory accesses are allowed during replay.
set record full -- Set record options.
set record full insn-number-max -- Set record/replay buffer limit.
set record full memory-query -- Set whether query if PREC cannot record memory change of next instruction.
set record full stop-at-limit -- Set whether record/replay stops when record/replay buffer becomes full.
set record function-call-history-size -- Set number of function to print in "record function-call-history".
set record instruction-history-size -- Set number of instructions to print in "record instruction-history".
set remote -- Remote protocol specific variables.
set remote TracepointSource-packet -- Set use of remote protocol `TracepointSource' (TracepointSource) packet.
set remote Z-packet -- Set use of remote protocol `Z' packets.
set remote access-watchpoint-packet -- Set use of remote protocol `Z4' (access-watchpoint) packet.
set remote agent-packet -- Set use of remote protocol `QAgent' (agent) packet.
set remote allow-packet -- Set use of remote protocol `QAllow' (allow) packet.
set remote attach-packet -- Set use of remote protocol `vAttach' (attach) packet.
set remote binary-download-packet, 
   set remote X-packet -- Set use of remote protocol `X' (binary-download) packet.
set remote breakpoint-commands-packet -- Set use of remote protocol `BreakpointCommands' (breakpoint-commands) packet.
set remote btrace-conf-bts-size-packet -- Set use of remote protocol `Qbtrace-conf:bts:size' (btrace-conf-bts-size) packet.
set remote btrace-conf-pt-size-packet -- Set use of remote protocol `Qbtrace-conf:pt:size' (btrace-conf-pt-size) packet.
set remote catch-syscalls-packet -- Set use of remote protocol `QCatchSyscalls' (catch-syscalls) packet.
set remote conditional-breakpoints-packet -- Set use of remote protocol `ConditionalBreakpoints' (conditional-breakpoints) packet.
set remote conditional-tracepoints-packet -- Set use of remote protocol `ConditionalTracepoints' (conditional-tracepoints) packet.
set remote ctrl-c-packet -- Set use of remote protocol `vCtrlC' (ctrl-c) packet.
set remote disable-btrace-packet -- Set use of remote protocol `Qbtrace:off' (disable-btrace) packet.
set remote disable-randomization-packet -- Set use of remote protocol `QDisableRandomization' (disable-randomization) packet.
set remote enable-btrace-bts-packet -- Set use of remote protocol `Qbtrace:bts' (enable-btrace-bts) packet.
set remote enable-btrace-pt-packet -- Set use of remote protocol `Qbtrace:pt' (enable-btrace-pt) packet.
set remote environment-hex-encoded-packet -- Set use of remote protocol `QEnvironmentHexEncoded' (environment-hex-encoded) packet.
set remote environment-reset-packet -- Set use of remote protocol `QEnvironmentReset' (environment-reset) packet.
set remote environment-unset-packet -- Set use of remote protocol `QEnvironmentUnset' (environment-unset) packet.
set remote exec-event-feature-packet -- Set use of remote protocol `exec-event-feature' (exec-event-fe--Type <RET> for more, q to quit, c to continue without paging--
ature) packet.
set remote exec-file -- Set the remote pathname for "run".
set remote fast-tracepoints-packet -- Set use of remote protocol `FastTracepoints' (fast-tracepoints) packet.
set remote fetch-register-packet, 
   set remote p-packet -- Set use of remote protocol `p' (fetch-register) packet.
set remote fork-event-feature-packet -- Set use of remote protocol `fork-event-feature' (fork-event-feature) packet.
set remote get-thread-information-block-address-packet -- Set use of remote protocol `qGetTIBAddr' (get-thread-information-block-address) packet.
set remote get-thread-local-storage-address-packet -- Set use of remote protocol `qGetTLSAddr' (get-thread-local-storage-address) packet.
set remote hardware-breakpoint-limit -- Set the maximum number of target hardware breakpoints.
set remote hardware-breakpoint-packet -- Set use of remote protocol `Z1' (hardware-breakpoint) packet.
set remote hardware-watchpoint-length-limit -- Set the maximum length (in bytes) of a target hardware watchpoint.
set remote hardware-watchpoint-limit -- Set the maximum number of target hardware watchpoints.
set remote hostio-close-packet -- Set use of remote protocol `vFile:close' (hostio-close) packet.
set remote hostio-fstat-packet -- Set use of remote protocol `vFile:fstat' (hostio-fstat) packet.
set remote hostio-open-packet -- Set use of remote protocol `vFile:open' (hostio-open) packet.
set remote hostio-pread-packet -- Set use of remote protocol `vFile:pread' (hostio-pread) packet.
set remote hostio-pwrite-packet -- Set use of remote protocol `vFile:pwrite' (hostio-pwrite) packet.
set remote hostio-readlink-packet -- Set use of remote protocol `vFile:readlink' (hostio-readlink) packet.
set remote hostio-setfs-packet -- Set use of remote protocol `vFile:setfs' (hostio-setfs) packet.
set remote hostio-unlink-packet -- Set use of remote protocol `vFile:unlink' (hostio-unlink) packet.
set remote hwbreak-feature-packet -- Set use of remote protocol `hwbreak-feature' (hwbreak-feature) packet.
set remote install-in-trace-packet -- Set use of remote protocol `InstallInTrace' (install-in-trace) packet.
set remote interrupt-on-connect -- Set whether interrupt-sequence is sent to remote target when gdb connects to.
set remote interrupt-sequence -- Set interrupt sequence to remote target.
set remote kill-packet -- Set use of remote protocol `vKill' (kill) packet.
set remote library-info-packet -- Set use of remote protocol `qXfer:libraries:read' (library-info) packet.
set remote library-info-svr4-packet -- Set use of remote protocol `qXfer:libraries-svr4:read' (library-info-svr4) packet.
set remote memory-map-packet -- Set use of remote protocol `qXfer:memory-map:read' (memory-map) packet.
set remote memory-read-packet-size -- Set the maximum number of bytes per memory-read packet.
set remote memory-tagging-address-check-packet -- Set use of remote protocol `qIsAddressTagged' (memory-tagging-address-check) packet.
set remote memory-tagging-feature-packet -- Set use of remote protocol `memory-tagging-feature' (memory-tagging-feature) packet.
set remote memory-write-packet-size -- Set the maximum number of bytes per memory-write packet.
set remote multiprocess-feature-packet -- Set use of remote protocol `multiprocess-feature' (multiprocess-feature) packet.
set remote no-resumed-stop-reply-packet -- Set use of remote protocol `N stop reply' (no-resumed-stop-reply) packet.
set remote noack-packet -- Set use of remote protocol `QStartNoAckMode' (noack) packet.
set remote osdata-packet -- Set use of remote protocol `qXfer:osdata:read' (osdata) packet.
set remote pass-signals-packet -- Set use of remote protocol `QPassSignals' (pass-signals) packet.
set remote pid-to-exec-file-packet -- Set use of remote protocol `qXfer:exec-file:read' (pid-to-exec-file) packet.
set remote program-signals-packet -- Set use of remote protocol `QProgramSignals' (program-signals) packet.
--Type <RET> for more, q to quit, c to continue without paging--
set remote query-attached-packet -- Set use of remote protocol `qAttached' (query-attached) packet.
set remote read-aux-vector-packet -- Set use of remote protocol `qXfer:auxv:read' (read-aux-vector) packet.
set remote read-btrace-conf-packet -- Set use of remote protocol `qXfer:btrace-conf' (read-btrace-conf) packet.
set remote read-btrace-packet -- Set use of remote protocol `qXfer:btrace' (read-btrace) packet.
set remote read-fdpic-loadmap-packet -- Set use of remote protocol `qXfer:fdpic:read' (read-fdpic-loadmap) packet.
set remote read-sdata-object-packet -- Set use of remote protocol `qXfer:statictrace:read' (read-sdata-object) packet.
set remote read-siginfo-object-packet -- Set use of remote protocol `qXfer:siginfo:read' (read-siginfo-object) packet.
set remote read-watchpoint-packet -- Set use of remote protocol `Z3' (read-watchpoint) packet.
set remote reverse-continue-packet -- Set use of remote protocol `bc' (reverse-continue) packet.
set remote reverse-step-packet -- Set use of remote protocol `bs' (reverse-step) packet.
set remote run-packet -- Set use of remote protocol `vRun' (run) packet.
set remote search-memory-packet -- Set use of remote protocol `qSearch:memory' (search-memory) packet.
set remote set-register-packet, 
   set remote P-packet -- Set use of remote protocol `P' (set-register) packet.
set remote set-working-dir-packet -- Set use of remote protocol `QSetWorkingDir' (set-working-dir) packet.
set remote software-breakpoint-packet -- Set use of remote protocol `Z0' (software-breakpoint) packet.
set remote startup-with-shell-packet -- Set use of remote protocol `QStartupWithShell' (startup-with-shell) packet.
set remote static-tracepoints-packet -- Set use of remote protocol `StaticTracepoints' (static-tracepoints) packet.
set remote supported-packets-packet -- Set use of remote protocol `qSupported' (supported-packets) packet.
set remote swbreak-feature-packet -- Set use of remote protocol `swbreak-feature' (swbreak-feature) packet.
set remote symbol-lookup-packet -- Set use of remote protocol `qSymbol' (symbol-lookup) packet.
set remote system-call-allowed -- Set if the host system(3) call is allowed for the target.
set remote target-features-packet -- Set use of remote protocol `qXfer:features:read' (target-features) packet.
set remote thread-events-packet -- Set use of remote protocol `QThreadEvents' (thread-events) packet.
set remote thread-options-packet -- Set use of remote protocol `QThreadOptions' (thread-options) packet.
set remote threads-packet -- Set use of remote protocol `qXfer:threads:read' (threads) packet.
set remote trace-buffer-size-packet -- Set use of remote protocol `QTBuffer:size' (trace-buffer-size) packet.
set remote trace-status-packet -- Set use of remote protocol `qTStatus' (trace-status) packet.
set remote traceframe-info-packet -- Set use of remote protocol `qXfer:traceframe-info:read' (traceframe-info) packet.
set remote unwind-info-block-packet -- Set use of remote protocol `qXfer:uib:read' (unwind-info-block) packet.
set remote verbose-resume-packet -- Set use of remote protocol `vCont' (verbose-resume) packet.
set remote verbose-resume-supported-packet -- Set use of remote protocol `vContSupported' (verbose-resume-supported) packet.
set remote vfork-event-feature-packet -- Set use of remote protocol `vfork-event-feature' (vfork-event-feature) packet.
set remote write-siginfo-object-packet -- Set use of remote protocol `qXfer:siginfo:write' (write-siginfo-object) packet.
set remote write-watchpoint-packet -- Set use of remote protocol `Z2' (write-watchpoint) packet.
set remoteaddresssize -- Set the maximum size of the address (in bits) in a memory packet.
set remotecache -- Set cache use for remote targets.
set remoteflow -- Set use of hardware flow control for remote serial I/O.
--Type <RET> for more, q to quit, c to continue without paging--
set remotelogbase -- Set numerical base for remote session logging.
set remotelogfile -- Set filename for remote session recording.
set remotetimeout -- Set timeout limit to wait for target to respond.
set remotewritesize -- Set the maximum number of bytes per memory write packet (deprecated).
set schedule-multiple -- Set mode for resuming threads of all processes.
set scheduler-locking -- Set mode for locking scheduler during execution.
set script-extension -- Set mode for script filename extension recognition.
set serial -- Set default serial/parallel port configuration.
set serial baud -- Set baud rate for remote serial I/O.
set serial parity -- Set parity for remote serial I/O.
set solib-search-path -- Set the search path for loading non-absolute shared library symbol files.
set source -- Generic command for setting how sources are handled.
set source open -- Set whether GDB should open source files.
set stack-cache -- Set cache use for stack access.
set startup-quietly -- Set whether GDB should start up quietly.
set startup-with-shell -- Set use of shell to start subprocesses.  The default is on.
set step-mode -- Set mode of the step operation.
set stop-on-solib-events -- Set stopping for shared library events.
set struct-convention -- Set the convention for returning small structs.
set style -- Style-specific settings.
set style address, set style disassembler address -- Address display styling.
set style address background -- Set the background color for this property.
set style address foreground -- Set the foreground color for this property.
set style address intensity -- Set the display intensity for this property.
set style disassembler -- Style-specific settings for the disassembler.
set style disassembler comment -- Disassembler comment display styling.
set style disassembler comment background -- Set the background color for this property.
set style disassembler comment foreground -- Set the foreground color for this property.
set style disassembler comment intensity -- Set the display intensity for this property.
set style disassembler enabled -- Set whether disassembler output styling is enabled.
set style disassembler immediate -- Disassembler immediate display styling.
set style disassembler immediate background -- Set the background color for this property.
set style disassembler immediate foreground -- Set the foreground color for this property.
set style disassembler immediate intensity -- Set the display intensity for this property.
set style disassembler mnemonic -- Disassembler mnemonic display styling.
set style disassembler mnemonic background -- Set the background color for this property.
set style disassembler mnemonic foreground -- Set the foreground color for this property.
set style disassembler mnemonic intensity -- Set the display intensity for this property.
set style disassembler register -- Disassembler register display styling.
set style disassembler register background -- Set the background color for this property.
set style disassembler register foreground -- Set the foreground color for this property.
set style disassembler register intensity -- Set the display intensity for this property.
set style enabled -- Set whether CLI styling is enabled.
set style filename -- Filename display styling.
set style filename background -- Set the background color for this property.
set style filename foreground -- Set the foreground color for this property.
set style filename intensity -- Set the display intensity for this property.
set style function, set style disassembler symbol -- Function name display styling.
set style function background -- Set the background color for this property.
set style function foreground -- Set the foreground color for this property.
set style function intensity -- Set the display intensity for this property.
set style highlight -- Highlight display styling.
set style highlight background -- Set the background color for this property.
set style highlight foreground -- Set the foreground color for this property.
set style highlight intensity -- Set the display intensity for this property.
set style metadata -- Metadata display styling.
set style metadata background -- Set the background color for this property.
set style metadata foreground -- Set the foreground color for this property.
--Type <RET> for more, q to quit, c to continue without paging--
set style metadata intensity -- Set the display intensity for this property.
set style sources -- Set whether source code styling is enabled.
set style title -- Title display styling.
set style title background -- Set the background color for this property.
set style title foreground -- Set the foreground color for this property.
set style title intensity -- Set the display intensity for this property.
set style tui-active-border -- TUI active border display styling.
set style tui-active-border background -- Set the background color for this property.
set style tui-active-border foreground -- Set the foreground color for this property.
set style tui-border -- TUI border display styling.
set style tui-border background -- Set the background color for this property.
set style tui-border foreground -- Set the foreground color for this property.
set style tui-current-position -- Set whether to style text highlighted by the TUI's current position indicator.
set style variable -- Variable name display styling.
set style variable background -- Set the background color for this property.
set style variable foreground -- Set the foreground color for this property.
set style variable intensity -- Set the display intensity for this property.
set style version -- Version string display styling.
set style version background -- Set the background color for this property.
set style version foreground -- Set the foreground color for this property.
set style version intensity -- Set the display intensity for this property.
set substitute-path -- Add a substitution rule to rewrite the source directories.
set suppress-cli-notifications -- Set whether printing notifications on CLI is suppressed.
set sysroot, set solib-absolute-prefix -- Set an alternate system root.
set target-charset -- Set the target character set.
set target-file-system-kind -- Set assumed file system kind for target reported file names.
set target-wide-charset -- Set the target wide character set.
set tcp -- TCP protocol specific variables.
set tcp auto-retry -- Set auto-retry on socket connect.
set tcp connect-timeout -- Set timeout limit in seconds for socket connection.
set tdesc -- Set target description specific variables.
set tdesc filename -- Set the file to read for an XML target description.
set trace-buffer-size -- Set requested size of trace buffer.
set trace-commands -- Set tracing of GDB CLI commands.
set trace-notes -- Set notes string to use for current and future trace runs.
set trace-stop-notes -- Set notes string to use for future tstop commands.
set trace-user -- Set the user name to use for current and future trace runs.
set trust-readonly-sections -- Set mode for reading from readonly sections.
set tui -- TUI configuration variables.
set tui active-border-mode -- Set the attribute mode to use for the active TUI window border.
set tui border-kind -- Set the kind of border for TUI windows.
set tui border-mode -- Set the attribute mode to use for the TUI window borders.
set tui compact-source -- Set whether the TUI source window is compact.
set tui mouse-events -- Set whether TUI mode handles mouse clicks.
set tui tab-width -- Set the tab width, in characters, for the TUI.
set unwind-on-signal, 
   set unwindonsignal -- Set unwinding of stack if a signal is received while in a call dummy.
set unwind-on-terminating-exception -- Set unwinding of stack if std::terminate is called while in call dummy.
set unwind-on-timeout -- Set unwinding of stack if a timeout occurs while in a call dummy.
set use-coredump-filter -- Set whether gcore should consider /proc/PID/coredump_filter.
set use-deprecated-index-sections -- Set whether to use deprecated gdb_index sections.
set variable, set var -- Evaluate expression EXP and assign result to variable VAR.
set verbose -- Set verbosity.
set watchdog -- Set watchdog timer.
set width -- Set number of characters where GDB should wrap lines of its output.
set write -- Set writing into executable and core files.
--Type <RET> for more, q to quit, c to continue without paging--
undisplay -- Cancel some expressions to be displayed when program stops.
whatis -- Print data type of expression EXP.
with, w -- Temporarily set SETTING to VALUE, run COMMAND, and restore SETTING.
x -- Examine memory: x/FMT ADDRESS.

Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) 
(gdb) 
(gdb) disassemble 
No frame selected.
(gdb) disassemble debugger0_a
No symbol table is loaded.  Use the "file" command.
(gdb) help
List of classes of commands:

aliases -- User-defined aliases of other commands.
breakpoints -- Making program stop at certain points.
data -- Examining data.
files -- Specifying and examining files.
internals -- Maintenance commands.
obscure -- Obscure features.
running -- Running the program.
stack -- Examining the stack.
status -- Status inquiries.
support -- Support facilities.
text-user-interface -- TUI is the GDB text based interface.
tracepoints -- Tracing of program execution without stopping the program.
user-defined -- User-defined commands.

Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) help running
Running the program.

List of commands:

advance -- Continue the program up to the given location (same form as args for break command).
attach -- Attach to a process or file outside of GDB.
continue, fg, c -- Continue program being debugged, after signal or breakpoint.
detach -- Detach a process or file previously attached.
detach checkpoint -- Detach from a checkpoint (experimental).
detach inferiors -- Detach from inferior ID (or list of IDS).
disconnect -- Disconnect from a target.
finish, fin -- Execute until selected stack frame returns.
handle -- Specify how to handle signals.
inferior -- Use this command to switch between inferiors.
interrupt -- Interrupt the execution of the debugged program.
jump, j -- Continue program being debugged at specified line or address.
kill -- Kill execution of program being debugged.
kill inferiors -- Kill inferior ID (or list of IDs).
next, n -- Step program, proceeding through subroutine calls.
nexti, ni -- Step one instruction, but proceed through subroutine calls.
queue-signal -- Queue a signal to be delivered to the current thread when it is resumed.
reverse-continue, rc -- Continue program being debugged but run it in reverse.
reverse-finish -- Execute backward until just before selected stack frame is called.
reverse-next, rn -- Step program backward, proceeding through subroutine calls.
reverse-nexti, rni -- Step backward one instruction, but proceed through called subroutines.
reverse-step, rs -- Step program backward until it reaches the beginning of another source line.
reverse-stepi, rsi -- Step backward exactly one instruction.
run, r -- Start debugged program.
signal -- Continue program with the specified signal.
start -- Start the debugged program stopping at the beginning of the main procedure.
starti -- Start the debugged program stopping at the first instruction.
step, s -- Step program until it reaches a different source line.
stepi, si -- Step one instruction exactly.
taas -- Apply a command to all threads (ignoring errors and empty output).
target -- Connect to a target machine or process.
target core -- Use a core file as a target.
target ctf -- (Use a CTF directory as a target.
target exec -- Use an executable file as a target.
target extended-remote -- Use a remote computer via a serial line, using a gdb-specific protocol.
target native -- Native process (started by the "run" command).
target record-btrace -- Collect control-flow trace and provide the execution history.
target record-core -- Log program while executing and replay execution from log.
target record-full -- Log program while executing and replay execution from log.
target remote -- Use a remote computer via a serial line, using a gdb-specific protocol.
target tfile -- Use a trace file as a target.
task -- Use this command to switch between Ada tasks.
task apply -- Apply a command to a list of tasks.
task apply all -- Apply a command to all tasks in the current inferior.
tfaas -- Apply a command to all frames of all threads (ignoring errors and empty output).
thread, t -- Use this command to switch between threads.
thread apply -- Apply a command to a list of threads.
thread apply all -- Apply a command to all threads.
thread find -- Find threads that match a regular expression.
thread name -- Set the current thread's name.
until, u -- Execute until past the current line or past a LOCATION.

Type "help" followed by command name for full documentation.
Type "apropos word" to search for commands related to "word".
--Type <RET> for more, q to quit, c to continue without paging--
Type "apropos -v word" for full documentation of commands related to "word".
Command name abbreviations are allowed if unambiguous.
(gdb) 
(gdb) r debugger0_a
Starting program: /home/kali/Downloads/debugger0_a debugger0_a
zsh:1: permission denied: /home/kali/Downloads/debugger0_a
During startup program exited with code 126.
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb) Quit
(gdb) exit
```
OK firstly installing gdb kinda got me, like i was typing the wrong command and i felt soo dumb that time. you might notice that i was lost in manual of gdb command, I tried to understand what command to use so i looked up the second hint which was to main is actually a recognized symbol that can be used with gdb commands.

so i mean i knew that if i need to find whats stored in eax then i need to see the assembly dump of the program because when i ran the file command on it, its a executable file.

when i analysed the dump i found that eax register has the value 0x86342 which is 549698 in decimal

```
FLAG-picoCTF{549698}

```



