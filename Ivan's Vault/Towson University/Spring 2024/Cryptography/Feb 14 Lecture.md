
- hw due next week


# Euclid's Extended Algorithm

## Goal
The primary goal is to find inverses throughout the course.

## Solving the Equation
Solve the equation modulo 43:

$$
\begin{align*}
13x + 12 &\equiv 21 \pmod{43} \\
13x + 12 - 12 &\equiv 21 - 12 \pmod{43} \\
13x &\equiv 9 \pmod{43}
\end{align*}
$$

## Using Euclid's Algorithm to Find $13^{-1} \pmod{43}$
Given \(gcd(43, 13) = 1\), we proceed as follows:

$$
\begin{align*}
43 &\equiv 3(13) + 4 \\
13 &\equiv 3(4) + 1 \\
4 &\equiv 4(1) + 0 \\\\
4 &= 43 - 3(13) \\
1 &= 13 - 3(4)
\end{align*}
$$

$$
\begin{align*}
1 &= 13 - 3(43 - 3(13)) \\
&= 13 - 3(43) + 9(13) \\
1 &= 10(13) - 3(43) \\\\
1 &\equiv 10(13) - 3(43) \pmod{43} \\\\
3(43) \pmod{43} &\equiv 0 \\\\
1 &\equiv 10(13) \pmod{43} \\
10 &\equiv 13^{-1} \pmod{43} \\\\
13x + 12 &\equiv 21 \pmod{43} \\
13x &\equiv 9 \pmod{43} \\
10(13x) &\equiv 10(9) \pmod{43} \\
x &\equiv 90 \pmod{43} \\
x &\equiv 4 \pmod{43}
\end{align*}
$$

Additional Equation:

$$
\begin{align*}
2x &\equiv 4 \pmod{6}\\
x &= 2 \pmod{6} \\
x &= 5 \pmod{6}
\end{align*}
$$

---

## Encoding Messages
- Moving forward, we will no longer encode letters/messages from 0 to 25.
- We will encode messages in binary, utilizing ASCII for conversions (e.g., A -> 65, Space -> 32).

## Types of Ciphers
- **Stream Ciphers**: Similar to affine ciphers.
- **Block Ciphers**: Similar to the hill cipher.

### Stream Cipher Setup
Generate a key (binary string) and encrypt by XORing $\oplus$ the key with the plaintext. This is addition $pmod{2}$ without carries.

#### XOR Operations
$$
\begin{align*}
0 \oplus 0 &= 0 \\
1 \oplus 0 &= 1 \\
0 \oplus 1 &= 1 \\
1 \oplus 1 &= 0
\end{align*}
$$

#### Example
Plaintext: `011010`  
Key: `101010`  
Encryption $E(x) = x \oplus k$:

$$
\begin{align*}
011010 \\
\oplus 101010 \\
\_\_\_\_\_\_\_\_ \\
110000
\end{align*}
$$

Note: In mod 2, addition and subtraction are the same operation because \(-1 \equiv 1 \pmod{2}\).

Decryption $D(x) = x \oplus k$ follows the same principle.

### One-Time Pad
- The key (\(k\)) is randomly generated and used only once.
- Exhibits perfect secrecy: every plaintext is equally likely to correspond to any ciphertext.

#### Disadvantages
- The key length is equal to the plaintext length and can only be used once.
- Securely transmitting the key is as challenging as transmitting the message.

## Generating Truly Random Numbers
- Often the weakest link in cryptography.

### Random Number Generators
- **Linear Congruential Random Number Generator (LCRNG)**: Used by systems like `java.random`.
    - Choose a modulus and two numbers $a$ and $b$, then use: $r_{i} \equiv a r_{i-1} + b \pmod{m}$ with a random seed $r_0$.

#### Example
Given $m = 11$, $a = 5$, $b = 7$, and $r_0 = 2$:

$$
\begin{align*}
r_1 &\equiv 5(2) + 7 \pmod{11} \equiv 17 \pmod{11} = 5 \\
r_2 &\equiv 5(5) + 7 \pmod{11} \equiv 32 \pmod{11} = 10 \\
r_3 &\equiv 5(10) + 7 \pmod{11} \equiv 57 \pmod{11} = 2
\end{align*}
$$

### Better RNG (Not Cryptographically Secure)
- **Linear Feedback Shift Register (LFSR)**: Generates new bits using the previous $k$ bits.

![[LSFR Script]]
