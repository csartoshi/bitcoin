Self-study of [Grokking Bitcoin by Kalle Rosenbaum](https://rosenbaum.se/book/grokking-bitcoin.html#ch02)

# Chapter 2. Cryptographic hash functions and digital signatures

This chapter covers:
  * Creating a simple money system: cookie tokens
  * Understanding cryptographic hash functions
  * Authenticating payments using digital signatures
  * Keeping your secrets secret

## 2.2.7. Exercises

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

u02 09

The four properties are also repeated as follows:

* The same input will always produce the same hash.

* Slightly different inputs will produce very different hashes.

* The hash is always of the same fixed size. For SHA256, it’s 256 bits.

* Brute-force trial and error is the only known way to find an input that gives a certain hash.

Let’s go back to the example where you had a cat picture on your hard drive and wrote down the cryptographic hash of the picture on a piece of paper. Suppose someone wanted to change the cat picture on your hard drive without you noticing. What variant of the fourth property is important for stopping the attacker from succeeding?

u02 10
