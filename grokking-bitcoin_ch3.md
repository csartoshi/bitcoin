
Self-study of [Grokking Bitcoin by Kalle Rosenbaum](https://rosenbaum.se/book/grokking-bitcoin.html#ch02)

[681,899 BH](https://blockstream.info/block/0000000000000000000c174b03714668052ca14887ba5b92d474b92792f1d13c)

# Chapter 3. Addresses

![ch3 fig51](https://github.com/thechipexpert/bitcoin/blob/main/images/ch03-recap2.svg)

## 3.7. Exercises

### 3.7.1. Warm up

The PKH is shorter than the public key—only 160 bits. We made it shorter using RIPEMD160. Why do you want it to be shorter? There are two good reasons.
> Shorter PKH uses less blockchain space and results in a lighter weight blockchain that is faster to download and store across a P2P network.

Base58check encoding is used to create a cookie token (Bitcoin) address from a PKH. Is it possible to reverse this process to create a PKH from an address?
> Yes, Base58check encoding is NOT a one-way hash function.  It is easily reversible between address <--> PKH.

When is base58check decoding used, and by whom?
> Base58check decoding is used by someone to verify/check for any typos with a PKH before that person sends a message to the PKH.  If you perform a Base58check decode and the checksum does not match the checksum of sha256(sha256((versioned PKH))) then the PKH was corrupted.

Base58 encode the two hex bytes 0047. Use the following diagram. You may skip this exercise if you didn’t read the section on base58 encoding.

![ch3 fig51](https://github.com/thechipexpert/bitcoin/blob/main/images/ch03-fig51.svg)

> 1. Remove leading 00 byte and count 
> 2. Convert to decimal number 4*(16^1) + 7*(16^0) = 71
> 3. Divide by 58.  71/58 = 1 r13
> 4. Divide quotient by 58. 1/58 = 0 r1
> 5. Lookup table: r13 + r1 = E2
> 5. Add 1 for every 00 byte: E21
> 6. Reverse order: 12E

What in an address makes it mostly safe from typing errors?
> Checksum (last 4 bytes) 

### 3.7.2. Dig in

Imagine that John wants a cookie from the cafe. He has two addresses: @1 with a balance of 5 CT, and @2 with 8 CT. His total balance is 13 CT, so he should be able to afford 10 CT for a cookie. Give an example of how he could pay 10 CT to the cafe.
> John would need to send a payment to the cafe with two inputs, one from each address.  He could send 5CT from @1 and 5 CT from @2 with 3 CT change returning to him.

Is it possible to deduce what cookie token addresses were involved in a certain payment by looking at the following spreadsheet?
![ch3 fig51](https://github.com/thechipexpert/bitcoin/blob/main/images/ch03-recap1.svg)
> Yes, because you can Base58 encode each PKH above to see which CT addresses were involved.

Is it possible to deduce what public keys were involved in a certain payment by looking at just the spreadsheet?
> No, because the spreadsheet is recording only the public key hashes (PKH) of each user.  

Suppose everybody always used unique addresses for each payment. What information from the spreadsheet could Acme use to roughly identify the cafe’s addresses?
> Acme could identify the PKH with the most frequent payments sent to it to infer which PKH belongs to the cafe.

Suppose there was a serious flaw in the public key derivation function, so anyone could calculate the private key from a public key. What prevents a bad guy from stealing your money in this scenario?

![ch3 fig51](https://github.com/thechipexpert/bitcoin/blob/main/images/ch03-recap4.svg)
> The PKH is a double-hash (SHA256 & RIPEMD160) of the public key.  So the attacker would not be able to derive the public key from the PKH in order to steal funds.

Suppose there was a serious flaw in RIPEMD160, so anyone could easily figure out a 256-bit pre-image of the PKH. This would mean it wasn’t pre-image resistant. What prevents a bad guy from stealing your money in this scenario?
> The pre-image resistance of SHA256 would still prevent the attacker from determining the 256-bit pre-image of the RIPEMD160(PKH).  The public key derivation function (ECDSA) also prevents the attacker from determining the private key from the public key.
