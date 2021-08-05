# Common Modulus

## What is RSA? And why does it matter?
![image](https://user-images.githubusercontent.com/65077960/127724300-1ef305ce-40a8-45ae-96d2-607146a92eee.png)

RSA (named after Rivest-Shamir-Adleman) is a public-key cryptosystem, used in modern applications. RSA implementations can be found in a wide range of places such as:
* PGP encryption
* SSL
* digital signatures  

and more.   
While common modulus attacks are uncommon in real-world scenarios, they are found in CTFs or other hacking challenges.

## Scenario
I'll set the scene with three characters. Steve, Tom and Julie. Steve has a message he needs to send to Tom but Julie keeps eavesdropping.
Steve and Tom use RSA encryption with Tom's public key (n, e^1). Unexpectedly a bit is flipped and the message is encrypted with a faulty public key. (n, e^2).  

Julie gets a holds of these and knows she can get the clear text using two different ciphertexts of the same message. Each encrypted with a different exponent but a common modulus.

message 1:
  ct₁ = E₍ₙ, ₑ₁₎(M)

message 2:
  ct₂ = E₍ₙ, ₑ₂₎(M)

If ct₂ = E₍ₙ, ₑ₂₎(M) == 1 and gcd(ct₂, n) == 1. She can recover the plaintext.  

## Deep diving into the less fun parts

Let's start by understanding the math behind RSA encrpytion. The formula for RSA enryption is as follows:
```
C = M^c mod n
```
[Bezout's theorem](https://en.wikipedia.org/wiki/B%C3%A9zout%27s_theorem) states that if the integers a and b (assuming they're both none-zeros). Then x and y are such that:  

```
ra + yb = gcd(a,b)
```
Finally, I'll revise division in modular arithmetic (oh boy does that sound exciting). A multiplicative inverse of a in mod n is x, where x is given by the following equation and can also be written as a^-1
```
ax = 1 (mod n)
```
For example, if we're operating in mod (Z₇) . The fraction 1/2(2^-1) is in the multiplicative inverse of 2. In which is 4 (2 x 4 = 1 (mod 7)). 
According to Bezout, if the denominator a and the modulus n are not [co-primes](https://byjus.com/maths/co-prime-numbers/) then the denominator is not invertible mod n. 1/a is invalid, like dividing by 0.

## Back to the fun part
Okay so, how do we actually use this? it's not as complex as the previous section made it sound.
If gcd(e1,e2) == 1, we have x and y such that: 
![image](https://user-images.githubusercontent.com/65077960/128417836-d642f614-aabd-4bb7-8c42-9adab441abaa.png)

Now using [Extended Euclidean algorithm](https://brilliant.org/wiki/extended-euclidean-algorithm/), we can find x and y then easily retrieve the plain text.  
All math below is perform in the common modulo:  
![image](https://user-images.githubusercontent.com/65077960/128417909-cf25a02b-8d5d-4bd0-afbd-5ee3c3e9bd3e.png)

If we deep dive into the equation, it gets a little more complicated to evaluate, y will normally be negative. C^y must be evaluated according to this:  
![image](https://user-images.githubusercontent.com/65077960/128417956-8031a7c0-60a3-443b-b668-222e820fd7aa.png)

As previously stated, for that fraction to be valid, C₂ must be invertible in mod n. gcd(C₂,n)=1 must also hold. Our final equation to recover the plaintext is:
![image](https://user-images.githubusercontent.com/65077960/128418004-96f4f728-67b1-45f7-9d4b-eca410d58e79.png)

Doing this on pen and paper is beyond time-consuming. Luckily this is pretty easy to do it in python and there's plenty of scripts available to do it. 
Here is one that I liked:  
https://github.com/HexPandaa/RSA-Common-Modulus-Attack
 



