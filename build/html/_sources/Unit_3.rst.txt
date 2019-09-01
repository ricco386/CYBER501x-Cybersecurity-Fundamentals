Unit 3
~~~~~~

* **Cryptography** is the practice and science of secure communication techniques.
* **Cryptanalysis** is the science of breaking cryptographic systems, codes, and algorithms.
* **Cryptology** refers to the scientific and mathematical study of both cryptography and cryptanalysis.
* **Plaintext** is a message or a file of any type in human readable form.
* Plaintext and a key, a string of 1s and 0s, are inserted into a cipher, an encryption algorithm that converts the plaintext into unreadable output known as **ciphertext**.

Algorithms are well-known, and they are never secret; keys are guarded and kept secret. Confidentiality depends fully on the key.

When you rely on the secrecy of the design and the implementation of a system as your security. Thinking you're achieving security like this is called security through obscurity. Kerckhoff's principle believes only secrecy of the key provides security.

Encryption comes in two forms, as do the keys:

Symmetric encryption
====================

uses one key, the same key for encrypting and decrypting. It's very fast, but there's a key distribution problem.

Older symmetric encryption algorithms include DES, 3DES, and RC4. Advanced Encryption Standard, AES, is the government-adopted and worldwide symmetric encryption algorithm used today.

Asymmetric encryption
=====================

uses two keys, one called a public key, the other one called a private key. When you encrypt with the public key, the ciphertext can only be decrypted with the private key. When you encrypt with a private key, the ciphertext can only be decrypted with the public key.

RSA -- named after its inventors Rivest, Shamir, and Adleman -- is the most widely used asymmetric encryption algorithm. It's used for SSL/TLS -- secure sockets layer/transport layer security.

Hashing
=======

Hashing provides integrity that messages that are sent are the messages that are received. Hashing makes sure no bits have been changed either accidentally or maliciously in transit. Hashing algorithms have a few characteristics:

* Different size of input, produce the same size output (message digest)
* If one bit in the input changes, the resulted hash is completely different.
* Hashes are called one-way functions because it's not feasible to try all possible combinations in a realistic amount of time.

Hashing standards:

* MD5 and more recently SHA-1 should be retiredand because it becomes easy to find multiple inputs that produce the same output message digest.
* SHA-2s, SHA-256 and SHA-512 and even SHA-3 variants are not appropriate for passwords because they're too quick for hackers attempting brute force attacks with today's graphics processing units.
* PBKDF2. Bcrypt and Scrypt which use SHA functions as part of their algorithms as well as Argon2 should be the only functions used for hashing passwords. Because this key stretching functions are significantly slower with tens or hundreds of thousands additional rounds.

Certificate Authority
=====================

A certificate authority or CA is a corporation that issues digital certificates. A CA is a trusted third party. Both CA Client and its visitors need to trust CA for the system to work. Symantec, Comodo, and GoDaddy are the top three certificate authorities today.

The CA constructs a digital certificate, signs it, and gives it to Client to put in the root of their web server. When a visitor goes to the bank's website, Client presents this digital certificate to the visitor.
