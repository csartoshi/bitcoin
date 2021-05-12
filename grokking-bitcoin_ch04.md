
Self-study of [Grokking Bitcoin by Kalle Rosenbaum](https://rosenbaum.se/book/grokking-bitcoin.html#ch04)

[683,322 BH](https://blockstream.info/block/00000000000000000008fa97446a5c97f916f31f2102a6ff8b8f7a5133390491)

# Chapter 4. Wallets

## 4.10.1. Warm up

4.1 Suppose you use a bitcoin wallet app and want to receive 50 BTC from your friend to your Bitcoin address 155gWNamPrwKwu5D6JZdaLVKvxbpoKsp5S. Construct a payment URI to give to your friend. Hint: in Bitcoin, the URI starts with bitcoin: instead of ct:. Otherwise, they’re the same.
> bitcoin:155gWNamPrwKwu5D6JZdaLVKvxbpoKsp5S?amount=50

4.2 How many coin flips does a random password of 10 characters correspond to? The password is selected from a 64-character alphabet.
> Each character represents 6 bits of entropy because 64 = 2^6 characters and there are 10 characters.  Therefore 6 x 10 = 60 bits of entropy, equivalent to 60 coin flips.

4.3 Name a few problems with password-protected backups. There are at least four.
> 1.  More things to secure: the password must be secured in addition to the backup seed/file.
> 2.  Forgotten password: If the password is rarely used, it is likely to be forgotten.
> 3.  Techn advancements: More advanced hardware and software will make it easier to crack passwords over time.
> 4.  Randomness is hard: Humans are bad at generating randomness compared to other methods - rolling dice, flipping coin, etc.

4.4 What three major steps are involved when a seed is created in an HD wallet that uses mnemonic sentences? You only need to answer this on a high level.
> 1.  First the seed is hashed with SHA256 (hex-based) and the first 4 bits of the has are appended to the seed as a check-sum.
> 2.  The binary hash value is arranged in 11-bit groupings.
> 3.  Convert binary 11-bit groupings to decimal and lookup mnemonic words from BIP39 2,048 words list, with a check-sum word at the end.

4.5 What does an xprv consist of?
> An xprv consists of the left 256 bits of a HMAC-SHA512 hash value of the seed.  The right 256 bits of the hash value becomes the chain code.

4.6 What does an xpub consist of?
> An xpub consists of a public key and the chain code (right 256 bits of the HMAC-SHA512 hash value of the seed).  Child xpubs consist of the public key derived from the child xprv and public key addition via ECC.

4.7 Suppose you want to make a hardened xprv with index 7 from m/2/1. What information do you need to create m/2/1/7'?
> You need the xprv (left half hash) at m/2/1 index 7 to calculate m/2/1/7'

4.8 Can you derive xpub M/2/1/7' from M/2/1? If not, how would you derive M/2/1/7'?
> No, you cannot derive a hardened child xpub from a parent xpub.  You must have the parent xprv at m/2/1 to generate a child xprv at m/2/1/7' using hardened xprv derivation and then calculate the xpub at M/2/1/7' from m/2/1/7'.

## 4.10.2. Dig in
4.9 Suppose you’re a bad guy and have the master xpub of a clueless victim. You’ve also stolen the private key m/4/1 that contains 1 BTC. Assume you also know this private key has this specific path. Describe how you’d go about calculating the master xprv. 
Use these hints:
![ch4 p4.9](https://github.com/thechipexpert/bitcoin/blob/main/images/ch04-p4.9.svg)

> 1. m/4/1 - "left half hash of index 1" = m/4
> 2. Derive xpub M/4 and chain code from the master xpub
> 3. Calculate the master xprv from m/4 - "left hash of index 4" = m

4.10 Suppose instead that your clueless victim had 0 bitcoins on the private key m/4/1, but plenty of money on other addresses under the same xprv. Would you be able to steal any money?
> Yes, because the xprv is not hardened it is possible to calculate the other addresses under the same xprv.

4.11 Suggest a better approach your victim could have used to prevent you from stealing all the money.
> Hardened child xprv derivation by hashing with the private key instead of the public key.

4.12 Say the cafe owner wants employees to have access to the counter sales account because they must be able to create a new address for each sale. But they must not have access to the private keys because the owner doesn’t trust the employees to handle them securely. Suggest how to achieve this. Hint: a wallet can import an xpub.
> Import a hardened xpub indexed at a certain value to your counter sales account wallet.  The counter sales account will be able to generate new addresses for each sale but will not have access to the master xpub or master xprv.

4.13 Suppose you work at the cafe and have loaded an xpub into your wallet. Your colleague Anita has loaded the same xpub into her wallet. You can both request payments from customers that go into the same account. How would you notice when Anita has received money into a previously empty key? Hint: you can create keys ahead of time.

![ch4 p4.13](https://github.com/thechipexpert/bitcoin/blob/main/images/ch04-p4.13.svg)

> You can generate addresses ahead of time and sync your wallets via the blockchain.  As Anita receives payments to the first address, your wallet will update and use the next address in the list.
