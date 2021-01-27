# Week 2: Cryptology

## Symmetric Encryption

### Cryptography

**Encryption** is the act of taking a message -- called *plaintext* -- and applying an operation to it -- called a *cipher* -- so that you receive a garbled, unreadable message as the output, called *ciphertext*.

The reverse process is called **decryption**.

A cipher is made of two components:
1. The **encryption algorithm**
  - The underlying logic or process that's used to convert the plaintext into ciphertext
2. The key
  - The key introduces something unique into your cipher; without the key, anyone using the same algorithm would be able to decode your message, and the secrecy would be lost.

**Security through obscurity:** If no one knows what algorithm or general security practice we're using, we're safer from attackers.

#### Kerchoff's principle

**Cryptosystem:** A collection of algorithms for key generation and encryption and decryption operations that comprise a cryptographic service should remain secure -- even if everything about the system is known, except the key.

This means that even if your enemy knows the exact encryption algorithm you use to secure your data, they're still unable to recover the plaintext from an intercepted ciphertext.

This principle is also known as *Shannon's maxim*, or *"The enemy knows the system."*

The system should remain secure even if your adversary knows exactly what kind of encryption systems you're employing, as long as *your keys remain secure*.

#### Cryptology

- The practice of coding and hiding messages from third parties is called **cryptography**
- The *study* of this practice is referred to as **cryptology**
- The opposite -- looking for hidden messages, or trying to decipher coded messages -- is known as **cryptanalysis**

**Frequency analysis** is the practice of studying the frequency with which letters appear in a ciphertext.

**Steganography** is the practice of hiding information from observers, but not encoding it.
- Archaic forms of stenography included invisible ink
- Modern steganographic techniques include embedding messages and even files into other files (like videos or images)
  - Fed into stenographic software, it would extract a hidden message within the image file.


### Symmetric Cryptography

**Symmetric-key algorithms** use the same key to encrypt and decrypt messages.

A **substitution cipher** is an encryption mechanism that replaces parts of your plaintext with ciphertext.

**Caesar cipher** is a well-known substitution cipher, which is a substitution alphabet.

**ROT13** where the alphabet is rotated 13 places; is actually a Caesar cipher using a key of 13.

**Block ciphers:** The cipher takes data in, places it into a bucket or block of data that's a fixed size, then encodes that entire block as one unit. (If the data to be encrypted isn't big enough to fill the block, the extra space will be padded to ensure the plaintext fits into the blocks evenly.)


**Stream ciphers:** Takes a stream of input and encrypts the stream one character or one digit at a time, outputting one encrypted character or digit at a time. (Meaning there is a 1:1 relationship to data in and data out.)

- Generally speaking, stream ciphers are faster; but can be less secure than block ciphers if the key isn't handled carefully and/or reused.
- To avoid key re-use, **initialization vector (IV)** is used
  - That's a bit of random data that's integrated into the encryption key and the resulting combined key is then used to encrypt the data.
  - The idea is if you have one shared master key, then generate a one-time encryption key
  - In order for the encrypted message to be decoded, the IV must be sent in plaintext along with the encryption message.


### Symmetric Encryption Algorithms

[ notes ]


## Public Key or Asymmetric Encryption

### Asymmetric Cryptography

The strength of the asymmetric encryption system comes from the computational difficulty of figuring out the corresponding private key, given a public key.

The three concepts that an asymmetric cryptosystem grants us are:
1. Confidentiality
  - Granted through the encryption/decryption mechanism
2. Authenticity
  - Granted through the digital signature mechanism
3. Non-repudiation
  - The author of the message isn't able to dispute the origin of the message

#### Symmetric vs Asymmetric Encryption
- Symmetric encryption algorithms are faster, more efficient at encrypting large amounts of data
- Asymmetric encryption works very well in untrusted environments; but it's computationally more expensive and complex
- Combined, asymmetric encryption can be used to keep a shared secret secure in transit; and after receiving the secret, using a symmetric encryption cipher to send data quickly and efficiently.

#### MACs

**Message Authentication Codes:** A bit of information that allows authentication of a received message, ensuring that the message came from the alleged sender and not a third party.

This is different from digital signatures, in that *the secret key that's used to generate the MAC is the same one that's used to verify it*.

**HMAC:** Keyed-hash authentication code. HMAC uses a cryptographic hash function along with a secret key to generate a MAC.

The MAC is sent alongside the message that's being checked; the MAC is verified by the receiver by performing the same operation on the received message, then comparing the computed MAC with the one received with the message. If they match, the message is authenticated.

**Cipher-Based Message Authentication Codes (CMACS):** Similar to HMACs, but instead of using a hashing function, a symmetric cipher with a shared key is used to encrypt the message, and the resulting output is used as the MAC.

**Cipher block chaining message authentication codes (CBC-MAC):** A CMAC example that's slightly different, building MACs using block ciphers. It encrypts using a block cipher in CBC mode, an operating mode for block ciphers that incorporates a previously encrypted block cipher text into the next block's plain text. So it builds a chain of encrypted blocks that requires the full, unmodified chain to decrypt.


### Asymmetric Encryption Algorithms

RSA

DSA

DH

Elliptic curve cryptography (ECC)
- The benefit of elliptic curve-based encryption is that it's able to achieve security similar to traditional public key systems with smaller key sizes.
- A 256-bit elliptic curve key would be comparable to a 3,072-bit RSA key.
- ECDH and ECDSA
- The NSA uses 384-bit EC keys to protect up to "top secret" data.


## Hashing

### Hashing

**Hashing (or a hash function)** is a type of function or operation that takes in an arbitrary data input and maps it to an output of fixed size, called a hash or digest.

You feed in any amount of data into a hash function and the resulting output will always be the same size; but the output should be *unique to the input*, such that two different inputs should never yield the same output.

Hashing can also be used to identify duplicate data sets in databases or archives to speed up searching of tables or to remove duplicate data to save space.

Cryptographic hash functions are used for various applications like:
- Authentication
- Message integrity
- Fingerprinting
- Data corruption deletion
- Digital signatures

*Cryptographic hashing is distinctly different from encryption because cryptographic hash functions should be one directional.*
- You can't take the hash output and recover the plain text

The ideal cryptographic hash function should be deterministic, meaning that the same input value should always return the same hash value.

- The function should not allow for **hash collisions** -- two different inputs mapping to the same output.

Cryptographic hash functions are very similar to symmetric key block ciphers in that they operate on blocks of data -- in fact, many popular hash functions are actually based on modified block ciphers.

`md5sum`


### Hashing Algorithms

- **MD5** is popular and wildly-used, designed in the early 1990s as a cryptographic hashing function
  - It operates on 512-bit blocks, and generates 128-bit hash digests
  - Towards 1996, MD5's flaws became more apparent, as it is vulnerable to hash collisions
  - This led to professionals recommending the adoption of...
- **SHA1** is part of the Secure Hash Algorithm suite of functions, designed by the NSA, published in 1995
  - It operates on 512-bit blocks, and generates 160-bit hash digests
  - SHA1 is used in protocols such as TLS/SSL, PGP SSH, and IPsec
  - SHA1 is also used in version control systems like Git
    - Git uses hashes to identify revisions and ensure data integrity by detecting corruption or tampering
  - SHA1 is being phased out for SHA2 and SHA3

Message Integrity Check (MIC) is a hash digest of the message in question, not unlike a checksum. It doesn't use secret keys (which means the 

#### MIC
- A **Message Integrity Check (MIC)** is essentially a hash digest of a message in question, much like a checksum to ensure that the contents of the message weren't modified in transit. 
- But unlike a MAC, it doesn't use secret keys -- there's nothing stopping an attacker from altering the message, recomputing the checksum, and modifying the MIC attached to the message.
- MICs protect against accidental corruption or loss, but not against malicious action or tampering.


### Hashing Algorithms (continued)

A successful brute force attack, against even the most secure system imaginable, is a function of attacker time and resources.

#### Rainbow Tables
- A **rainbow table** is a pre-computed table of all possible password values and their corresponding hashes. 
- The idea behind rainbow table attacks is to trade computational power for disk space by pre-computing the hashes and storing them in a table
- The idea behind these types of attacks is to trade computational power for disk space, by pre-computing the hashes and storing them in a table.
- An attacker can determine what the corresponding password is for a given hash by just looking up the hash in their rainbow table.
- This is unlike a brute force attack, where the hash is computed for each guess attempt.
- You can protect against rainbow table attacks with salts.

#### Salts
- A **Password salt** is additional randomized data that's added into the hashing function to generate a hash that's unique to the password and salt combination.
- This makes it so that an attacker would have to compute a rainbow table for each possible salt value
- If a large salt is used, the computational and storage requirements to generate useful rainbow tables becomes almost unfeasible.
- Early Unix systems used a 12-bit salt, which amounts to a total of 4,096 possible salts;
  - Modern systems like Linux, BSD, and Solaris use a 128-bit salt
  - 128-bit salt makes it so that rainbow table attacks aren't possible in any realistic timeframe.


## Cryptography Applications

### Public Key Infrastructure

- **Public Key Infrastructure (PKI)** is a system that defines the creation, storage, and distribution of digital certificates.
  - A *digital certificate* is a file that proves an entity owns a certain public key.
  - A certificate contains information about the public key, the entity it belongs to, and a digital signature from another party that has verified this information.
- The entity that's responsible for storing, issuing, and signing certificates is referred to as **Certificate authority (CA)**.
- There's also a **Registration authority (RA)** who's responsible for verifying the identities of any entities requesting certificates to be signed and stored with the CA.

A central repository is needed to securely store and index keys; and a certificate management system of some sort makes managing access to stored certificates and issuance of certificates easier.

- SSL/TLS server certificate
- Self-signed certificate
- SSL/TLS client certificate
  - Optional and less commonly seen than server certificates
  - These are certificates that are bound to clients and are used to authenticate the client to the server, allowing access control to an SSL/TLS service.
- Code signing certificates are used for signing executable programs
  - This allows users of these signed applications to verify the signatures and ensure that the application was not tampered with

#### Certificate authority trust
- Begins with the Root Certificate Authority
  - There are no higher authorities than them, so they self-sign on their behalf
- 
- A certificate that has no authority as a CA is referred to an **end-entity** or **leaf certificate**.
  - Named because it's the fringe, like a leaf on a tree, as opposed to the root of the tree.

#### X.509
- The **X.509 standard** is what defines the format of digital certificates.
- The fields defined in an X.509 certificate are:
  - Version: What version of the X.509 standard the certificate adheres to
  - Serial number: A unique identifier for the certificate assigned by the CA, which allows the CA to manage and identify individual certificates
  - Certificate signature algorithm: Indicates what public key algorithm is used for the public key and what hashing algorithm is used to sign the certificate
  - Issuer name: Information about the authority that signed the certificate
  - Validity: This contains two subfields -- "Not Before" and "Not After" -- which define the dates when the certificate is valid for
  - Subject: Information about the entity the certificate was issued to
  - Subject Public Key Info: Two subfields define the algorithm of the public key, along with the public key itself
  - Certificate Signature Algorithm: Same as the Subject Public Key Info field; these two fields must match
  - Certificate Signature Value: The digital signature data itself

Fingerprints are hash digests of the whole certificate; they're not actual fields in the certificate, but are computed by clients when validating or inspecting certificates.

#### Web of Trust
= An alternative to the centralized PKI model of establishing trust and binding identities
- A Web of Trust is where individuals -- instead of certificate authorities -- sign other individuals' public keys
- Usually, people interested in establishing web of trusts will organize *key signing parties* where participants perform the same verification and signing.


### Cryptography in Action

TLS grants us 3 things:

- handshake

The session key is the shared symmetric encryption key used in TLS sessions to encrypt data being sent back and forth. Since this key is derived from the public-private key, if the private key is compromised, there's potential for an attacker to decode all previously transmitted messages that were encoded using keys derived from this private key.

Forward secrecy

- Secure Shell (SSH)
- Pretty Good Privacy (PGP)
  - PGP is very secure, with no known mechanisms to break the encryption, and is comparable to military-grade encryption.


### Securing Network Traffic

- If you want to protect data in transit, but the application/channel doesn't utilize encryption, the solution is a VPN.
- A **Virtual private network (VPN)** is a mechanism

OpenVPN authentication methods support pre-shared secrets, certificate-based, and username/passwords.


### Cryptographic Hardware

- **Trusted Platform Module (TPM)**
  - A hardware device that's typically integrated into a computer
  - A dedicated crypto-processor
  - Has a unique, secret RSA key burned into the hardware
  - TMP offers:
    - Secure generation of keys
    - Random number generation
    - Remote attestation
      - The idea of a system authenticating its software and hardware configuration to a remote system.
    - Data binding and sealing
      - This involves using the secret key to derive a unique key, that's then used for encryption of data.
      - This basically binds encrypted data to the TPM; the system the TPM is installed in sends only the keys stored in hardware in the TPM will be able to decrypt the data.

- TPM is a standard with several revisions
- The most secure implementation of TPM is the *discrete chip*, as these incorporate physical tampering resistance to prevent physical attacks on the chip.
- **Secure element:** A tamper-resistant chip often embedded in the microprocessor, or integrated into the mainboard of a mobile device. It supplies secure storage of cryptographic keys and provides a secure environment for applications.

- Trusted Execution Environment (TEE)

- Full Disk Encryption (FDE)
  - Options include:
    - PGP (a commercial product)
    - Bitlocker (from Microsoft; integrates well with TPMs)
    - Filevault 2 (from Apple)
    - dm-crypt (open source for Linux)

- Random vs Pseudo-Random
- **Entropy Pool:** A source of random data to help seed random number generators.
