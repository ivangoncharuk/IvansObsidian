
## Caesar Cipher

### Encryption Function
$$E_k(X) \equiv x + k \pmod{26}$$
$$k \rightarrow \text{key}$$
### Decryption Function
$$D_k(x) \equiv x - k \pmod{26}$$

### Why is it easy to decrypt?
- Because it has only 26 possible keys
- Very easy to brute force

## Modular Arithmetic

- We say that $a \equiv b \pmod{m}$
- "a is congruent to b modulo m"

*if $a$ and $b$ have the same remainder when divisible by $m$*

Alternatively...

$a \equiv b \pmod{m}$
if $m$ divides $(a - b)$

As long as you perform the same operation top both sides of a congruence equation it will still be true. (just like equals)

$$5 \equiv 31 \equiv -21 \pmod{26}$$

Addition, subtraction, and multiplication are always valid in modular arithmetic
Be careful with division...

We are never allowed to write fractions in modular arithmetic

$\pmod m$ the only numbers are things equivalent to $0, 1, 2, \dots m - 1$

## Affine Cipher (Souping up Caesar Cipher)

Caesar Cypher is too easy...lets introduce something more secure.

Pick a key $(a, b)$
- b can be anything $\pmod{26}$
- a has some restrictions...

### Example

Encryption function $E(x) \equiv ax + b \pmod{26}$

- $E(x) = 3x + 11 \pmod{26}$
- a = 3
- b = 11

encrypting `"it"`
- `i`$\rightarrow 8$
- `t`$\rightarrow 19$

$$
\begin{align*}
	E(8) &\equiv 3(8) + 11 \\
	&\equiv 24+11 \\
	&\equiv 35 \\
	&\equiv 9 \pmod{26}
\end{align*}
$$

$$\begin{align*}
	E(8) &\equiv 3(19) + 11 \\
	&\equiv 57+11 \\
	&\equiv 68 \\
	&\equiv 16 \pmod{26}
\end{align*}
$$


**`"it"` encrypts to `"JQ"`**

### How to decrypt affine cipher?

$$y_{\text{cipher text}} \equiv 
E(x) \equiv 
ax_{\text{plain text}}+b \pmod{26}$$
1. Subtract b from both sides
$$y - b\equiv 
E(x) \equiv 
ax \pmod{26}$$
2. Divide a to both sides...this wouldn't work because we cannot easily divide with modular arithmetic. to "divide" we multiply both sides by the `inverse` of $a$
$$
\begin{align*}
	a^{-1}(y - b) 
	&\equiv a^{-1}(ax) \\
	&\equiv (a^{-1}a)x \\
	&\equiv x \pmod{26}
\end{align*}
$$
The inverse of a, $a^{-1} \pmod{26}$ (if it exists) is a number where $a*a^{-1} \equiv 1 \pmod{26}$

### Decryption function

$$
\begin{align*}
D(y) &\equiv a^{-1}(y-b) \\
&\equiv  a^{-1}y-a^{-1}b \pmod{26}
\end{align*}
$$

Find the decryption function for $E(x) \equiv 3x + 11 \pmod{26}$


$$
\begin{align*}
	E(x) &\equiv 3x + 11 \pmod{26} \\
	\rightarrow y &\equiv 3x + 11 \\\\
	3^{-1} &\equiv 9 \quad
	\text{because }3 \cdot 9 \equiv 27 \equiv 1 \\\\
	9(y-11) &\equiv 9(3x) \equiv x\\
	9y - 99 &\equiv x \\\\
	-99 &\equiv 5 \pmod{26} \\\\
	D(y) &\equiv 9y + 5 \pmod{26}
\end{align*}
$$

![[mod26_table.png || 700]]

$a$ has to be one of $\{1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25\}$

How many keys are there for the affine cipher?
- 12 possibilities for a
- 26 possibilities for b
$12 \times 26 = 312$ keys

You still can brute force it by hand but easier with a computer.


