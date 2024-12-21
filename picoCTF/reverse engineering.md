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


