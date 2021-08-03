# Intro
RSA (Rivest–Shamir–Adleman) is a public-key cryptosystem used for secure data transmission.
RSA was first publicaly described in 1977 by [Ron Rivest](https://en.wikipedia.org/wiki/Ron_Rivest), [Adi Shamir](https://en.wikipedia.org/wiki/Adi_Shamir) and [Leonard Adleman](https://en.wikipedia.org/wiki/Leonard_Adleman)
An equivelent system was developed in 1973 at [GCGQ](https://en.wikipedia.org/wiki/GCHQ) by [Clifford Cocks](https://en.wikipedia.org/wiki/Clifford_Cocks) and publically disclosed in the same year as RSA was first described.

# How does it work?
In a public-key cryptosystem, the encryption key is public and distinct from the decryption key (or the private key). A user creates and publishes a public key based on two large prime numbers, along with an auxilary value.
The prime numbers are kept secret and are difficult, if not impossible, to reverse. Messages can be encrypted by anyone with the public key but only decrypted by those with the two prime numbers. 

The actual security of RSA is dependent on the practical difficulty of factoring the product of the 2 primes. This where the [RSA problem](https://en.wikipedia.org/wiki/RSA_problem) comes in (more in it later). There are currently no published methods to break RSA, given a large neough key is used. Finding new prime numbers make this (among other cryptosystems) secure, hence the high payout for finding one (for example: https://en.wikipedia.org/wiki/Great_Internet_Mersenne_Prime_Search)

The process can be brown down into steps:  

* Choose any large prime number (A and B)
* N = A * B
* Select public key (E for encryption). Choose the key so that it is not a factory of (A-1) or (B-1)
* Select a private key (D for decryption). Choose the private key so that it matches this equation: (D\*E) mod (A-1) \* (B-1) = 1
* For encryption, calculate the ciphertext from the plaintext using this equation: CT = PT^E mod N
* For decryption we use: PT = CT^D mod N

## RSA Problem

The RSA proble summarizes the task of performing an RSA private-key operation given only the public key. The RSA algorithm raises a message to an exponent, modulo a composite number (N) whose factors are unknown. The task can be described as finding the e^th roots of an arbitrary number, modulo N. 
For larger RSA key sizes (1024 bits and above), no efficient method of solving this is known.

Let's say a system was found, the security of RSA-Based crytosystems would be jeopardized. The RSA problem is to efficiently compute P given an RSA public key (N, e) and ciphertext: C ≡ P^e (mod N). The structure of an RSA public key requires N be a large semiprime (such as the sum of 2 large primes), that 2 < e < N, that e be coprime to φ(N), and that 0 <= C < N. C is chosen randomly within that range.
