# Easy ROP challenge  

We'll be treating the ropeasy binary as an unknown binary, we have no context of what it does or how to exploit it. Like all things in hacking, we start with enumeration.  
Tools like [checksec](https://docs.pwntools.com/en/stable/commandline.html) can help us indenify potential attack vectors and understand where we might want to start:  

![checksecOutput](https://user-images.githubusercontent.com/65077960/127680041-8f0ecfcc-d9e4-47be-8673-6cc3966e39de.png)

We're currently itneresting in "No canary found". Typically a random value is generated at program initialization and inserted at the end of the high risk area where the stack overflows.
At the end of the function, it checks to see if the value has been modified. The binary is also statically linked, so we can assume the gadgets are available to us.  

Our first test is typically to run the binary and use it as intended. Look for inputs and outputs, understand how the binary might work:  
![image](https://user-images.githubusercontent.com/65077960/127681942-de961813-665b-4959-acd3-da4673c8c445.png)

![image](https://user-images.githubusercontent.com/65077960/127681981-32fa2a07-95b4-4181-bddb-7f23d13b564e.png)

If our input is too large, we get a segmentation fault:  
![image](https://user-images.githubusercontent.com/65077960/127682045-57738d79-a39a-4e9f-a7d0-f71b83a6d8de.png)





