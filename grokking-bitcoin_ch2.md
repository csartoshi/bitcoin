Self-study of [Grokking Bitcoin by Kalle Rosenbaum](https://rosenbaum.se/book/grokking-bitcoin.html#ch02)

[681,000 BH](https://blockstream.info/block/00000000000000000001b9e7f67b9cd2572d6f01d189bcef4c93cb4570bf1ee7)

# Chapter 2. Cryptographic hash functions and digital signatures

This chapter covers:
  * Creating a simple money system: cookie tokens
  * Understanding cryptographic hash functions
  * Authenticating payments using digital signatures
  * Keeping your secrets secret

## 2.2.7 Exercises

### Warm up

How many bits is the output of SHA256?
> 256 bits

How many bytes is the output of SHA256?
> 256/8 = 32 bytes

What’s needed to calculate the cryptographic hash of the text “hash me”?
> A cryptographic hash function such as *addition modulo 256* that wraps around to 0 when the sum of two numbers reaches 256.

What are the decimal and the binary representations of the hexadecimal data 061a?
> a x 1 = 10\
> 1 x 16 = 16\
> 6 x 16 x 16 = 1,536\
> 0 x 16 x 16 x 16 = 0\
> **1,562**

Can you, in practice, modify the text “cat” so the modified text gets the same cryptographic hash as “cat”?
> No, slightly different inputs will produce very different hashes (digests).

### Dig in

The simplistic hash function from Section 2.2.2, repeated for you as follows, isn’t a cryptographic hash function. Which two of the four properties of a cryptographic hash function is it lacking?

![ch2 fig24](https://github.com/thechipexpert/bitcoin/images/ch02-fig24.svg)

> Brute-force trial and error is NOT the only known way to find an input that gives a certain hash. 256 and 512 should give the same hash.

The four properties are also repeated as follows:

* The same input will always produce the same hash.

* Slightly different inputs will produce very different hashes.

* The hash is always of the same fixed size. For SHA256, it’s 256 bits.

* Brute-force trial and error is the only known way to find an input that gives a certain hash.

Let’s go back to the example where you had a cat picture on your hard drive and wrote down the cryptographic hash of the picture on a piece of paper. Suppose someone wanted to change the cat picture on your hard drive without you noticing. What variant of the fourth property is important for stopping the attacker from succeeding?

![ch2 fig26](https://github.com/thechipexpert/bitcoin/images/ch02-fig26.svg)

> Second pre-image resistance: I only have the cryptographic hash (digest) of the pre-image written down on a piece of paper.  It is really hard to find a second pre-image that matches my hash.

[681,896 BH](https://blockstream.info/block/00000000000000000003828302c6ca30275f680e9b3c4faf34d9dfa1e132c0aa)

## 2.5 Exercises

### 2.5.1 Warm Up

Lisa is currently rewarded 7,200 CT per day for her work. Why won’t the supply increase infinitely over time? Why don’t we have 7,200 × 10,000 = 72 million CT after 10,000 days?
> The CT supply is programmatically restricted to reduce by half at a predetermined interval.

How can coworkers detect if Lisa rewards herself too much or too often?
> The ledger is public for all to see.

How is the private key of a key pair created?
> The private key is generated from an extremely large random number.

What key is used to digitally sign a message?
> The private key is used to encrypt a message.

The signing process hashes the message to sign. Why?
> The signing process hashes the message to create a fixed length string that saves space in the blockchain.

What would Mallory need to steal cookie tokens from John?
> Mallory needs to steal John's private key to be able to digitally sign his messages and steal his CT.

### 2.5.2 Dig In

Suppose you have a private key and you’ve given your public key to a friend, Fred. Suggest how Fred can send you a secret message that only you can understand.
> Fred could write a message and encrypt it using my public key.  Then I would use my private key to decrypt and read the message.

Suppose you (let’s pretend your name is Laura) and Fred still have the keys from the previous exercise. Now you want to send a message in a bottle to Fred saying,

> Hi Fred! Can we meet at Tiffany’s at sunset tomorrow? /Laura

Explain how you would sign the message so Fred can be sure the message is actually from you. Explain what steps you and Fred take in the process.

> 1. Laura generates a private key and public key pair.
> 2. Write the message and digitally sign it with the private key.  This includes encrypting the message.
> 3. Use a cryptographic hash function to hash the message to a fixed length.
> 4. Send to Fred.
> 5. Fred decrypts and reads the message.
