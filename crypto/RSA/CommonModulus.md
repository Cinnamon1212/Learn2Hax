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

Julie gets a holds of these and knows she can get the clear text using two different ciphertexts of the same message. Each encrypted with a different exponent but a different modulus.

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

