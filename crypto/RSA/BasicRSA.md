# Intro
RSA (Rivest–Shamir–Adleman) is a public-key cryptosystem used for secure data transmission.
RSA was first publicaly described in 1977 by [Ron Rivest](https://en.wikipedia.org/wiki/Ron_Rivest), [Adi Shamir](https://en.wikipedia.org/wiki/Adi_Shamir) and [Leonard Adleman](https://en.wikipedia.org/wiki/Leonard_Adleman)
An equivelent system was developed in 1973 at [GCGQ](https://en.wikipedia.org/wiki/GCHQ) by [Clifford Cocks](https://en.wikipedia.org/wiki/Clifford_Cocks) and publically disclosed in the same year as RSA was first described.

# How does it work?
In a public-key cryptosystem, the encryption key is public and distinct from the decryption key (or the private key). A user creates and publishes a public key based on two large prime numbers, along with an auxilary value.
The prime numbers are kept secret and are difficult, if not impossible, to reverse. Messages can be encrypted by anyone with the public key but only decrypted by those with the two prime numbers. 
