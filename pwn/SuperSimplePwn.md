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

```



