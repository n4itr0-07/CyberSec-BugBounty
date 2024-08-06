# Cryptography and its Types



Cryptography is a technique of securing communication by converting plain text into ciphertext. It involves various algorithms and protocols to ensure data confidentiality, integrity, authentication, and non-repudiation. In this article, we will discuss cryptography and its types.

## What is Cryptography?

Cryptography is a technique of securing information and communications through the use of codes so that only those persons for whom the information is intended can understand and process it, thus preventing unauthorized access to information. The prefix “crypt” means “hidden” and the suffix “graphy” means “writing”. In Cryptography, the techniques that are used to protect information are obtained from mathematical concepts and a set of rule-based calculations known as algorithms to convert messages in ways that make them hard to decode. These algorithms are used for cryptographic key generation, digital signing, and verification to protect data privacy, web browsing on the internet, and to protect confidential transactions such as credit card and debit card transactions.


![cry](https://github.com/user-attachments/assets/d2cecf47-a28c-4572-bc46-a7436e581206)

## Features Of Cryptography

- **Confidentiality**: Information can only be accessed by the person for whom it is intended and no other person except him can access it.
- **Integrity**: Information cannot be modified in storage or transition between sender and intended receiver without any addition to the information being detected.
- **Non-repudiation**: The creator/sender of information cannot deny his intention to send information at a later stage.
- **Authentication**: The identities of the sender and receiver are confirmed, as well as the destination/origin of the information.
- **Interoperability**: Cryptography allows for secure communication between different systems and platforms.
- **Adaptability**: Cryptography continuously evolves to stay ahead of security threats and technological advancements.

## Types Of Cryptography

### 1. Symmetric Key Cryptography

It is an encryption system where the sender and receiver of a message use a single common key to encrypt and decrypt messages. Symmetric Key cryptography is faster and simpler, but the problem is that the sender and receiver have to exchange keys securely. The most popular symmetric key cryptography systems are Data Encryption Systems (DES) and Advanced Encryption Systems (AES).
![Symmetric Type](https://github.com/user-attachments/assets/ec1b7808-999e-475c-87ff-e6ce669fd9d2)


### 2. Hash Functions

There is no usage of any key in this algorithm. A hash value with a fixed length is calculated as per the plain text which makes it impossible for the contents of plain text to be recovered. Many operating systems use hash functions to encrypt passwords.

### 3. Asymmetric Key Cryptography

In Asymmetric Key Cryptography, a pair of keys is used to encrypt and decrypt information. A receiver’s public key is used for encryption and a receiver’s private key is used for decryption. Public keys and Private keys are different. Even if the public key is known by everyone, the intended receiver can only decode it because he alone knows his private key. The most popular asymmetric key cryptography algorithm is the RSA algorithm.


## Applications of Cryptography

- **Computer passwords**: Cryptography is widely utilized in computer security, particularly when creating and maintaining passwords. When a user logs in, their password is hashed and compared to the hash that was previously stored. Passwords are hashed and encrypted before being stored. In this technique, the passwords are encrypted so that even if a hacker gains access to the password database, they cannot read the passwords.
- **Digital Currencies**: To protect transactions and prevent fraud, digital currencies like Bitcoin also use cryptography. Complex algorithms and cryptographic keys are used to safeguard transactions, making it nearly impossible to tamper with or forge the transactions.
- **Secure web browsing**: Online browsing security is provided by the use of cryptography, which shields users from eavesdropping and man-in-the-middle assaults. Public key cryptography is used by the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols to encrypt data sent between the web server and the client, establishing a secure channel for communication.
- **Electronic signatures**: Electronic signatures serve as the digital equivalent of a handwritten signature and are used to sign documents. Digital signatures are created using cryptography and can be validated using public key cryptography. In many nations, electronic signatures are enforceable by law, and their use is expanding quickly.
- **Authentication**: Cryptography is used for authentication in many different situations, such as when accessing a bank account, logging into a computer, or using a secure network. Cryptographic methods are employed by authentication protocols to confirm the user’s identity and confirm that they have the required access rights to the resource.
- **Cryptocurrencies**: Cryptography is heavily used by cryptocurrencies like Bitcoin and Ethereum to protect transactions, thwart fraud, and maintain the network’s integrity. Complex algorithms and cryptographic keys are used to safeguard transactions, making it nearly impossible to tamper with or forge the transactions.
- **End-to-end Internet Encryption**: End-to-end encryption is used to protect two-way communications like video conversations, instant messages, and email. Even if the message is encrypted, it assures that only the intended receivers can read the message. End-to-end encryption is widely used in communication apps like WhatsApp and Signal, and it provides a high level of security and privacy for users.

## Types of Cryptography Algorithm

- **Advanced Encryption Standard (AES)**: AES (Advanced Encryption Standard) is a popular encryption algorithm that uses the same key for encryption and decryption. It is a symmetric block cipher algorithm with a block size of 128 bits, 192 bits, or 256 bits. The AES algorithm is widely regarded as the replacement for the DES (Data encryption standard) algorithm.
- **Data Encryption Standard (DES)**: DES (Data encryption standard) is an older encryption algorithm that is used to convert 64-bit plaintext data into 48-bit encrypted ciphertext. It uses symmetric keys (which means the same key for encryption and decryption). It is kind of old by today’s standards but can be used as a basic building block for learning newer encryption algorithms.
- **RSA**: RSA is a basic asymmetric cryptographic algorithm that uses two different keys for encryption. The RSA algorithm works on a block cipher concept that converts plain text into cipher text and vice versa.
- **Secure Hash Algorithm (SHA)**: SHA is used to generate unique fixed-length digital fingerprints of input data known as hashes. SHA variations such as SHA-2 and SHA-3 are commonly used to ensure data integrity and authenticity. The tiniest change in input data drastically modifies the hash output, indicating a loss of integrity. Hashing is the process of storing key-value pairs with the help of a hash function into a hash table.

## Advantages of Cryptography

- **Access Control**: Cryptography can be used for access control to ensure that only parties with the proper permissions have access to a resource. Only those with the correct decryption key can access the resource thanks to encryption.
- **Secure Communication**: For secure online communication, cryptography is crucial. It offers secure mechanisms for transmitting private information like passwords, bank account numbers, and other sensitive data over the Internet.
- **Protection against attacks**: Cryptography aids in the defense against various types of assaults, including replay and man-in-the-middle attacks. It offers strategies for spotting and stopping these assaults.
- **Compliance with legal requirements**: Cryptography can assist firms in meeting a variety of legal requirements, including data protection and privacy legislation.

## Conclusion

Cryptography is essential for protecting data and communications by converting plain text into ciphertext using various techniques. It maintains confidentiality, integrity, authenticity, and non-repudiation. Cryptography encompasses both symmetric and asymmetric key systems, as well as hash functions, and is essential in applications such as computer security, digital currencies, safe online browsing, and electronic signatures. It provides strong protection against unauthorized access and attacks, while constantly developing to address new security risks and advances in technology.

## Frequently Asked Questions on Cryptography – FAQs

**What is the purpose of Cryptography?**
The purpose of cryptography is to secure and protect sensitive information by encoding it in a way that only authorized parties can understand.

**What are Digital Signatures?**
Digital signatures are cryptographic techniques used to provide authentication, integrity, and non-repudiation for digital documents or messages.

**Can quantum computers break existing Cryptographic Systems?**
Quantum computers have the potential to break existing cryptographic systems due to their ability to solve certain mathematical problems much faster than traditional computers.

**How is Cryptography used in e-commerce transactions?**
Cryptography is used in e-commerce transactions to encrypt sensitive data, such as credit card information, during transmission to ensure its confidentiality and integrity.
