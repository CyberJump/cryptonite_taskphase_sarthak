
# Pondering Paths

#The Root-

To obtain the current flag of this challenge, we first have to just have to give the command of absolute address of file pwn which is /pwn

```bash
Connected!
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{kNynWJQTPbwl2LoJ6WzgKfapvei.dhzN5QDLzkTN0czW}
```

#Program and Absolute Paths-

To obtain this flag, we have to give the absolute path of /challenge/run

```bash
Connected!
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{UkEmb0ScD9U3vRWLt4JDzpiJLcr.dVDN1QDLzkTN0czW}
```
#Position thy self-

To obtain this flag, we have to first execute /challenge/run which will give the an the directory required to cd and then we have to cd /home after which we will pass the command /challenge/run

```bash
Connected!
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /home
hacker@paths~position-thy-self:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4a1Rvk4d3sN7pcDZwk1u9VFRsM6.dZDN1QDLzkTN0czW}
```
#Position elsewhere-

To obtain this flag, we have to first execute /challenge/run which will give the an the directory required to cd and then we have to cd /var after which we will pass the command /challenge/run

```bash
Connected!
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /var
hacker@paths~position-elsewhere:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{IGCVrU_10B73RZfRkoqoUn7XVH5.ddDN1QDLzkTN0czW}
```
#Position yet elsewhere-

To obtain this flag, we have to first execute /challenge/run which will give the an the directory required to cd and then we have to cd /etc/apt/sources.list.d after which we will pass the command /challenge/run

```bash
Connected!
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /etc/apt/sources.list.d directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /etc/apt/sources.list.d
hacker@paths~position-yet-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{Q7foMyLprBv5heLoop7O2c4usm0.dhDN1QDLzkTN0czW}
```
#implicit relative paths, from/ -

To obtain this flag, we have first have to cd to the directory / after which our CWD is / so then we execute the command challenge/run which the relative path

```bash
Connected!
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{ERv8cwWe07iqCRwpYs5TFnzM5yD.dlDN1QDLzkTN0czW}
```
#explicit relative paths, from/ -

To obtain this flag, we have first have to cd to the directory / after which our CWD is / so then we execute the command ./challenge/run which the explicit relative path of /challenge/run. As we . we give the parent directory of /challenge/run

```bash
Connected!
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{gWCcWUv3qIVV7yhlPlxHuiW_6p8.dBTN1QDLzkTN0czW}
```
#implicit relative paths -

To obtain this flag, we have first have to cd to the directory /challenge after which our CWD is /challenge  so then we execute the command ./run which the relative path of /run in the directory /challenge

```bash
Connected!
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{4o2QVhYFGa1vuck1gxNJw8j771Q.dFTN1QDLzkTN0czW}
```
#Home sweet Home -

To obtain this flag, we first have to understand the ~ symbol is shortform of the home directory and is the absolute path of /home/hacker. Now that we know what's ~ is for then in the challenge we have to pass the command /challenge/run with a argument which have obey 3 rules which are -

1)Your argument must be an absolute path. 

2)The path must be inside your home directory.

3)Before expansion, your argument must be three characters or less.

so when we pass a suitable argument the content of the file /challenge/run will be copied in that file and will be read out the flag.So we can pass argument like ~/p
```bash
Connected!
hacker@paths~home-sweet-home:~$ /challenge/run ~/p
Writing the file to /home/hacker/p!
... and reading it back to you:
pwn.college{YRlAMq32NeXW0NYrr59vWu-fwbj.dNzM4QDLzkTN0czW}
```

