---
tags:
  - spring2024
  - MATH-314
---

## Stream Cipher

Encrypts individual letters or bits - **one at a time**

(changing one letter or bit of plaintext only changes one letter of cipher-text)


## Block Cipher

- Multiple letters or bits are *joined* into a **block**.
- Entire **blocks** are encrypted at once
- Changing one letter of a block can change the entire block of ciphertext

### Hill Cipher

- Pick a *block* size $b$
- Break out plaintext into blocks

To encrypt a *block*, we convert it to a **vector** (write horizontally or **vertically**)

$$E(\vec{v}) = k\vec{v} \pmod{26}$$

Key is a $b \times b$ matrix of numbers $\pmod{26}$

#### Example

- $b = 2$
$$ k = 
\begin{bmatrix}
	3 & 4 \\
	14 & 7
\end{bmatrix}
$$



Encrypt `"math"`
`"ma"` $\rightarrow 12\ 0$ 
`"th"` $\rightarrow 19, 7$

$$
\begin{align*}
	E
	\left(
		\begin{bmatrix}
			12 \\ 0
		\end{bmatrix}
	\right)
	&=
	\begin{bmatrix}
		3 & 4 \\
		14 & 7
	\end{bmatrix}
	
	\begin{bmatrix}
		12 \\ 0
	\end{bmatrix} \\
	
	&\equiv
	
	\begin{bmatrix}
		3 \cdot 12 &+\ \ \ \ 4 \cdot 0 \\
		14 \cdot 12 &+\ \ \ \ 7 \cdot 0
	\end{bmatrix} \\
	
	&\equiv
	
	\begin{bmatrix}
		36 + 0 \\
		168 + 0
	\end{bmatrix} \\
	
	&\equiv
	
	\begin{bmatrix}
		10 \\ 12
	\end{bmatrix}
	
	\rightarrow
	
	\text{"KM"}
\end{align*}
$$


Do the same for `"TH"`


If we change one letter, the entire block changes


### Decrypt Hill Cipher

$$
\begin{align*}
	\vec{w} \equiv E(\vec{v}) &= k\vec{v} \\
	(&\text{Solve for }\vec{v})
\end{align*}
$$

to decrypt, $k$ needs to have an inverse $k^{-1}$

Multiply through by this inverse $k^{-1}w \equiv \cancel{\frac{k^{-1}}{k}}\vec{v}$


To decrypt a Hill Cipher, we use the equation:

$$
\vec{v} \equiv D(\vec{w}) \equiv K^{-1}(\vec{w}) \mod 26
$$

Where:
- $\vec{v}$ is the plaintext vector.
- $\vec{w}$ is the cipher-text vector.
- $D(\vec{w})$ is the decryption function applied to the ciphertext vector.
- $K^{-1}$ is the inverse of the key matrix $K$ used in the encryption, modulo 26.
- The operation is performed modulo 26 because we are working with the English alphabet, which has 26 letters.

To find the inverse of $K$ modulo 26, we need to ensure that $K$ is invertible in modulo 26, which means that the determinant of $K$, denoted as $\det(K)$, and 26 are coprime (i.e., their greatest common divisor is 1).

The formula to compute the inverse of $K$ in modulo 26 is given by:

$$
K^{-1} = \frac{1}{\det(K)\pmod{26}} \cdot \text{adj}(K) \pmod{26}
$$

Where:
- $\text{adj}(K)$ is the adjugate (or adjoint) of $K$.
- The division by $\det(K) \mod 26$ actually involves multiplying by the multiplicative inverse of $\det(K) \mod 26$ in the field of integers modulo 26.

Given a $2 \times 2$ key matrix $K$:

$$
K \equiv \begin{bmatrix}
c & d \\
e & f
\end{bmatrix}
$$

The inverse $K^{-1}$ modulo 26 can be calculated as:

$$
K^{-1} \equiv \frac{1}{cf-ed \pmod{26}} \cdot 
\begin{bmatrix}
f & -d \\
-e & c
\end{bmatrix} \pmod{26}
$$
$$
K^{-1} = (cf-ed)^{-1} \cdot 
\begin{bmatrix}
f & -d \\
-e & c
\end{bmatrix} \pmod{26}
$$

After finding $K^{-1}$, we can decrypt $\vec{w}$ to get $\vec{v}$ using the first equation.

### In Python


```python
R = IntegerModRing(26)
K = matrix(R, [[3, 4], [14, 7]])
print(K)
print(K * vector([12, 0]))
print()
print(K^-1)
K^-1 * vector([10, 12])
K^-1 * vector([7, 3])

# [ 3  4]
# [14 7]
# (10 12)

# [ 5 12]
# [16 17]
# (12, 0)
# (19, 7)

```



### Attacking the Hill Cipher

#### Known Plaintext Attack

In a known plaintext attack against the Hill Cipher with a block size of 2, we aim to determine the entries of the encryption matrix. This method requires having a pair of plaintext and its corresponding ciphertext. Using matrix algebra, we can solve for the encryption matrix.

Suppose the word `"Linear"` encrypts to `"LTPVPI"` using a Hill Cipher with block size 2. We can represent the plaintext and ciphertext in numerical form (assuming A=0, B=1, ..., Z=25) as follows:

| Plaintext | num | Ciphertext | num |
| --------- | --- | ---------- | --- |
| L         | 11  | L          | 11  |
| I         | 8   | T          | 19  |
| N         | 13  | P          | 15  |
| E         | 4   | V          | 21  |
| A         | 0   | P          | 15  |
| R         | 17  | I          | 8   | 

By combining blocks to form matrices from the plaintext (P) and ciphertext (C), we create an equation of matrices. For example, taking the first two plaintext blocks "LI" and "NE", and their corresponding ciphertext "LT" and "PV", we form:

- For "LI" and "LT":
$$
P = \begin{bmatrix} 11 & 8 \\ 13 & 4 \end{bmatrix}, \quad C = \begin{bmatrix} 11 & 19 \\ 15 & 21 \end{bmatrix}
$$

To solve for the encryption matrix $K$, we use the equation $C \equiv PK \pmod{26}$. However, to find $K$, we first need to compute $P^{-1}$, the inverse of the plaintext matrix $P$, and then multiply it by $C$.

Calculating $P^{-1}$, we start by finding the determinant of $P$ and its inverse modulo 26. The determinant of $P$ is given by:

$$
\det(P) = 11 \cdot 4 - 8 \cdot 13 \equiv -60 \pmod{26}
$$

However, as noted, $-60 \equiv -8 \equiv 18 \pmod{26}$, and since 18 does not have a multiplicative inverse in modulo 26 (which is incorrect as every non-zero element of a finite field does have a multiplicative inverse), we encounter an error in the calculation. Let's correct this approach:

First, the correct approach should ensure that the determinant of $P$ has a multiplicative inverse modulo 26. The calculation mistake here is in the assumption that 18 does not have an inverse modulo 26, when in fact, every number that is coprime with 26 does have an inverse in modulo 26 arithmetic. 

Let's correct the process of finding $P^{-1}$ under modulo 26:

- Correct determinant calculation and its multiplicative inverse.
- Use the corrected determinant to find $P^{-1}$.
- Solve for $K$ by multiplying $P^{-1}$ with $C$.

#### Correcting $P^{-1}$ Calculation

1. Correct the determinant of $P$ and find its multiplicative inverse modulo 26.
2. Apply the formula for the inverse of a 2x2 matrix modulo 26, ensuring correct modular arithmetic application.
3. Finally, multiply the inverse of $P$ by $C$ to solve for the encryption matrix $K$.

Here, the correction and continuation of the process will depend on correctly applying modular arithmetic and ensuring the use of valid algebraic and modular operations. The step mentioning that $-60^{-1} \equiv -8^{-1} \equiv 18^{-1}$ and concluding that $P^{-1}$ doesn't exist due to a misunderstanding of modular arithmetic needs reevaluation.

To proceed correctly, let's actually calculate the determinant of $P$, its modulo 26 inverse, and then correctly apply these steps to find $K$.
