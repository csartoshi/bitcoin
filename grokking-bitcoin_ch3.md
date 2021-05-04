
Self-study of [Grokking Bitcoin by Kalle Rosenbaum](https://rosenbaum.se/book/grokking-bitcoin.html#ch02)

[681,899 BH](https://blockstream.info/block/0000000000000000000c174b03714668052ca14887ba5b92d474b92792f1d13c)

# Chapter 3. Addresses

## 3.7. Exercises

### 3.7.1. Warm up

The PKH is shorter than the public key—only 160 bits. We made it shorter using RIPEMD160. Why do you want it to be shorter? There are two good reasons.
> Shorter PKH uses less blockchain space and results in a lighter weight blockchain that is faster to download and store across a P2P network.

Base58check encoding is used to create a cookie token (Bitcoin) address from a PKH. Is it possible to reverse this process to create a PKH from an address?
> Yes, Base58check encoding is NOT a one-way hash function.  It is easily reversible between address <--> PKH.

When is base58check decoding used, and by whom?
> Base58check decoding is used by someone to verify/check for any typos with a PKH before that person sends a message to the PKH.  If you perform a Base58check decode and the checksum does not match the checksum of sha256(sha256((versioned PKH))) then the PKH was corrupted.

Base58 encode the two hex bytes 0047. Use the following diagram. You may skip this exercise if you didn’t read the section on base58 encoding.

![ch3 fig51](https://github.com/thechipexpert/bitcoin/blob/main/ch03-fig51.svg)

> 1. Remove leading 00 byte and count 
> 2. Convert to decimal number 4*(16^1) + 7*(16^0) = 71
> 3. Divide by 58.  71/58 = 1 r13
> 4. Divide quotient by 58. 1/58 = 0 r1
> 5. Lookup table: r13 + r1 = E2
> 5. Add 1 for every 00 byte: E21
> 6. Reverse order: 12E

What in an address makes it mostly safe from typing errors?
> Checksum (last 4 bytes) 

