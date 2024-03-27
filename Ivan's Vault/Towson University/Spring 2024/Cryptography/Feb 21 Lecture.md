---
tags:
  - MATH-314
  - spring2024
---

# Feb 21

## Properties of Modern Ciphers (Symmetric Key)

Symmetric key ciphers are foundational to cryptographic security. Their effectiveness is often evaluated based on two primary properties: confusion and diffusion. These properties work together to ensure the security and robustness of a cryptographic system.

### Confusion

- **Definition**: Confusion refers to the complexity of the relationship between the ciphertext and the key. This complexity ensures that an adversary cannot straightforwardly deduce the key through simple arithmetic or straightforward analysis.
- **Purpose**: The main goal of confusion is to make the relationship between the ciphertext and the key as intricate as possible, thwarting attempts to reverse-engineer the key from the ciphertext.

### Diffusion

- **Definition**: Diffusion is about the intricate relationship between the plaintext and the ciphertext. The principle dictates that even a minor change in the plaintext should lead to a significant and unpredictable change in the ciphertext.
- **Purpose**: The aim of diffusion is to disperse the plaintext information throughout the ciphertext, making it difficult for an attacker to deduce any information about the plaintext from the ciphertext.

### Examples and Historical Context

- **Hill Cipher**: Demonstrates a high level of diffusion as a small change in the plaintext results in a substantial alteration in the ciphertext. However, it lacks confusion since its operations do not sufficiently obscure the relationship between the key and the ciphertext.
- **Stream Ciphers**: Typically exhibit significant confusion, especially if the keystream generation mechanism is complex. However, they inherently lack diffusion because changes in the plaintext directly affect only the corresponding bits in the ciphertext without a broader impact.

### Evolution of Cryptographic Standards

- **Early Development**: In 1972, the National Bureau of Standards (NBS), now known as the National Institute of Standards and Technology (NIST), issued a request for proposals for a national cryptographic standard.
- **IBM's Contribution**: IBM submitted a cipher named LUCIFER, which they had been using internally.
- **NSA's Involvement**: The National Security Agency (NSA) proposed several modifications to LUCIFER, including the addition of complex permutations on the bits and alterations to the S-boxes, which are crucial for creating confusion.
- **DES Emergence**: The modified version of LUCIFER, after incorporating the NSA's changes, was officially named the Digital Encryption Standard (DES).
    - **S-boxes Explained**: S-boxes (Substitution-boxes) play a critical role in creating confusion within cryptographic systems. They operate by substituting input bits with output bits according to a predefined, complex, and seemingly random table, thereby significantly obfuscating the relationship between the ciphertext and the key.


## DES (Data Encryption Standard)

DES, a cornerstone of early cryptographic systems, operates on a structure known as a Feistel cipher. This structure is pivotal to its design and functionality.

### Feistel Cipher Overview

- **Core Concept**: A Feistel cipher encompasses several rounds of processing the plaintext, aiming to thoroughly mix the data with the key material.
- **Round Operations**: Each round splits the plaintext into two halves, denoted as left ($L_i$) and right ($R_i$), and processes them as follows:
    - The left half is moved to the right.
    - The right half undergoes a transformation by an $F$-function, which takes the left half and a round-specific key ($K_i$) as inputs, and then is XORed with the left half to produce the new left half for the next round.

The transformation for round $i$ is mathematically represented as:
$$R_{i+1} = L_i$$
$$L_{i+1} = R_i \oplus F(L_i, K_i)$$

- **Cipher Specification**: To define a cipher using the Feistel structure, you need to detail:
    - The number of rounds.
    - The specific operations of the $F$-function ($F(L, K)$).
    - The methodology for generating round keys from the master key.

### DES's Fundamental Flaw

- **Key Length**: The primary issue with DES was its master key length of only 56 bits. This was considered secure until advancements in computing made brute-force attacks feasible.
- **Brute-Force Vulnerability**: By 1998, collective efforts led to the creation of supercomputers capable of breaking a DES key through brute-force, demonstrating the need for longer key lengths.

### Evolution and Countermeasures

- **Usage Span**: DES was widely adopted from its inception in 1972 until the early 2000s. However, as computational capabilities increased, the security provided by DES's 56-bit keys became insufficient.
- **Brute-Force Mitigation**: To combat brute-force attacks, a method of using DES multiple times with different keys was employed. Double encryption, although intuitive, was found to be vulnerable to meet-in-the-middle attacks.
    - **Double Encryption**: Encrypting twice with two different keys ($K_1$ and $K_2$) seemed like a straightforward solution but only offered a marginal increase in security equivalent to adding a single bit to the key length.
    - **Meet-in-the-Middle Attack**: This attack strategy decrypts the ciphertext with one key while encrypting the plaintext with another, then compares the outputs to find a match, significantly reducing the effectiveness of double encryption.

### Triple Encryption

- **Introduction**: To address the limitations of double encryption, triple encryption was introduced, using two keys ($K_1$ and $K_2$) in a specific sequence to enhance security.
- **Triple DES (3DES)**: The process involves two encryptions with $K_1$, sandwiching an encryption with $K_2$, as shown below:
$$C = E_{K_1}( E_{K_2}(E_{K_1}(P)) )$$
- **Persistence**: Triple DES remained in use until the late 2010s, highlighting its effectiveness and the industry's gradual shift towards more secure standards like AES (Advanced Encryption Standard).

### Transition to AES

- **Next Steps**: Before delving into AES, it's essential to understand the concept of finite fields, which play a crucial role in the AES algorithm and its security properties.

## Finite Fields

Finite fields, also known as Galois fields, are fundamental structures in mathematics and cryptography, particularly in algorithms like the Advanced Encryption Standard (AES).

### Basic Concepts

- **Ring**: A set equipped with two operations, addition and multiplication, that satisfy certain axioms similar to those of integers. Division is not necessarily defined for all elements of a ring.
- **Field**: A ring in which every non-zero element has a multiplicative inverse. Fields support addition, subtraction, multiplication, and division (except by zero).

### Examples of Fields

- **Real Numbers ($\mathbb{R}$)**: Includes all possible values along the continuum of real numbers.
- **Rational Numbers ($\mathbb{Q}$)**: Consists of all fractions formed by integers, where the denominator is not zero.
- **Complex Numbers ($\mathbb{C}$)**: Encompasses numbers of the form $a + bi$, where $a$ and $b$ are real numbers, and $i$ is the square root of $-1$.

### Non-Examples

- **Integers ($\mathbb{Z}$)**: While integers form a ring, they do not constitute a field because not every element has a multiplicative inverse within the integers.

### Special Cases

- **Modular Arithmetic**: When considering integers modulo a number $n$, denoted as $\mathbb{Z}_n$, the structure forms a field only if $n$ is prime. This is symbolized as $\mathbb{Z}_p$ or $\mathbb{F}_p$, where $p$ is a prime number.
- **Finite Fields ($\mathbb{F}_n$)**: Represent fields with a finite number of elements $n$. There exists at most one field of any given size $n$, and a finite field $\mathbb{F}_p$ exists if and only if $p$ is prime.
    - **Notation**: Finite fields are also referred to as Galois Fields, denoted as $GF(n)$, highlighting their foundational role in Galois theory.

### Finite Fields in Cryptography

- **AES and Finite Fields**: The Advanced Encryption Standard (AES) utilizes arithmetic within $\mathbb{F}_{256}$ for its operations. This field, consisting of $256 = 2^8$ elements, is crucial for the algorithm's security and efficiency.
    - **Distinct from $\mathbb{Z}_{256}$**: The field $\mathbb{F}_{256}$ is not the same as performing arithmetic modulo 256. It involves more complex structures to ensure properties like closure under field operations.

### Importance

Finite fields provide the mathematical foundation for various cryptographic algorithms, enabling secure and efficient data encryption and decryption processes. The choice of field, such as $\mathbb{F}_{256}$ for AES, is essential for defining the operation of these algorithms and their resistance to cryptographic attacks.






