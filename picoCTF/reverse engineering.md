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


