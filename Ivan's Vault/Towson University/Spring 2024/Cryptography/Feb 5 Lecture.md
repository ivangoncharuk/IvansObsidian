---
tags:
  - MATH-314
  - spring2024
---

`Notes for Feb 5th MATH-314 lecture prepared by Ivan Goncharuk`
## Types of Attacks

### Eve's Activities

- **Cipher text only**
  - Eve only has access to the cipher text.
  - Obtaining the cipher-text is her initial goal.
  - The main objective is to decipher the key.

- **Known plaintext attack**
  - Eve is aware of a cipher-text and its corresponding plaintext.
  - The goal is to discover the key.

- **Chosen plaintext attack**
  - Eve can select a plaintext and observe the corresponding ciphertext.
  - The goal is to unearth the key.

## Attacking the Affine Cipher

- **Known plaintext attack**
  - Attempt all 312 keys through brute force.
  - Establish equations involving the key and solve them.

### Example

Suppose you learn that "in" encrypts to "BI" using an affine cipher:
- i becomes an 8
- n becomes a 13

The encryption equations are:
$$E(8) \equiv a \cdot 8 + b \equiv 1 \pmod{26}$$
$$E(13) \equiv a \cdot 13 + b \equiv 8 \pmod{26}$$

Subtracting these equations, we get:
$$
\begin{align*}
8a + b &\equiv 1 \pmod{26} \\
- (13a + b &\equiv 8 \pmod{26}) \\
\hline
-5a &\equiv -7 \pmod{26} \\
5a &\equiv 7 \pmod{26} \\
(21)(5a) &\equiv (21)(7) \pmod{26} \\
a &\equiv 147 \equiv 17 \pmod{26}
\end{align*}
$$

To find \(b\):
$$
\begin{align*}
17 \cdot 13 + b &\equiv 8 \pmod{26} \\
221 + b &\equiv 8 \pmod{26} \\
b &\equiv 8 - 221 \equiv -213 \equiv 21 \pmod{26} \\
\end{align*}
$$
Therefore, \(a = 17\) and \(b = 21\).

### What to Pick for Known Plaintext?

- Pick "a" (which converts to 0) as plaintext: \(E(0) \equiv a \cdot 0 + b $equiv b \pmod{26}$
- Pick "b": $(E(1) = a + b \pmod{26}$. Subtract $b$ to find $a$.

### Cipher-text Only

- **Brute force**: Try all 312 keys to see which one reveals a valid message.
- **Use letter frequencies** to make educated guesses.

## Substitution Cipher

- Utilize a key table for all 26 letters and their corresponding ciphertext letters.
- How many keys? \(26!\) for all possible combinations.

## Vigenère Cipher

![[Vigenère Cipher]]

## Finding Coincidences in Cipher-text

![[Finding Coincidences in Cipher-text]]




