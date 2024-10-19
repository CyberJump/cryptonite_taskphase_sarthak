
# Chaining Commands -

# Chaining with semicolons-

you can chain commands by using ; after the first command.For this challenge, we have to chain /challenge/pwn and /challenge/college

```bash
Connected!
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{ka6rlcN5X73uMsF2WerorIeMT6E.dVTN4QDLzkTN0czW}
```
# Your First Shell Script-

we can create a shell script to run commands by using .sh file.For this challenge, we have to create a x.sh shell script then nano it to edit it and bash it to run the script.

```bash
Connected!
hacker@chaining~your-first-shell-script:~$ touc x.sh
ssh-entrypoint: touc: command not found
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ nano x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{cdo5FMN65j8PmWUrgnz3IcHZzp9.dFzN4QDLzkTN0czW}
```
# Redirecting Script Output-

Just like normal commands shell script can be piped and everything. For this challenge we have to pipe the previous challenge script output to input of /challenge/solve.

```bash
Connected!
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ nano x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{A6I4qH69qp5_h9izLdlS-rrQooX.dhTM5QDLzkTN0czW}
```
# Executable Shell scripts-

we can make a shell script executable without use of bash by chmod its permission to be executable.For this challenge we have to make a shell script with /challenge/solve and run it without using bash.

```bash
Connected!
hacker@chaining~executable-shell-scripts:~$ touch script.sh
hacker@chaining~executable-shell-scripts:~$ nano script.sh
hacker@chaining~executable-shell-scripts:~$ chmod ugo+rwx script.sh
hacker@chaining~executable-shell-scripts:~$ ./script.sh
Congratulations on your shell script execution! Your flag:
pwn.college{Ur5_zCiR0N_jEXxZhQl8uUK8CJJ.dRzNyUDLzkTN0czW}
```