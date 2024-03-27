---
tags:
  - MATH-314
  - spring2024
---


## Question 1
Encrypt the messages $\texttt{cook}$ and $\texttt{book}$ using the Hill cipher with $m=2$ and 
$$K = 
\left(\begin{array}{cc}
2 & 5 \\
3 & 11 \\
\end{array}\right)
$$

$$
\begin{align*}
m &= 2 \\
K &= 

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix} \\\\
\texttt{cook} &\rightarrow C = 2, O = 14, O = 14, K = 10 \rightarrow 
\begin{bmatrix}
	2 \\
	14 \\
\end{bmatrix} \texttt{and} 
\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix} \\\\

\texttt{book} &\rightarrow B = 1, O = 14, O = 14, K = 10 \rightarrow 
\begin{bmatrix}
	1 \\
	14 \\
\end{bmatrix} \texttt{and} 
\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix} \\\\

\end{align*}
$$
$$
K \times
\begin{bmatrix}
	x \\
	y \\
\end{bmatrix} \equiv

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix}

\times

\begin{bmatrix}
	x \\
	y \\
\end{bmatrix}

\equiv

\begin{bmatrix}
	(2x+5y) \pmod{26} \\
	(3x + 11y) \pmod{26} \\
\end{bmatrix}
$$

$$
\texttt{"co"} \rightarrow 
\begin{bmatrix}
	2 \\
	14 \\
\end{bmatrix}

\rightarrow

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix}

\times

\begin{bmatrix}
	2 \\
	14 \\
\end{bmatrix}

\begin{bmatrix}
	(2(2)+5(14)) \pmod{26} \\
	(3(2) + 11(14)) \pmod{26} \\
\end{bmatrix}

\equiv

\begin{bmatrix}
	22 \\
	4 \\
\end{bmatrix}

\rightarrow \texttt{"VE"}
$$
$$

\texttt{"ok"} \rightarrow 
\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix}

\rightarrow

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix}

\times

\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix}

\begin{bmatrix}
	(2(14)+5(10)) \pmod{26} \\
	(3(14) + 11(10)) \pmod{26} \\
\end{bmatrix}

\equiv

\begin{bmatrix}
	0 \\
	22 \\
\end{bmatrix}

\rightarrow \texttt{"AW"}
$$
$$
E(\texttt{"cook"}) \rightarrow \texttt{"VEAW"}
$$

$$
\texttt{"bo"} \rightarrow 
\begin{bmatrix}
	1 \\
	14 \\
\end{bmatrix}

\rightarrow

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix}

\times

\begin{bmatrix}
	1 \\
	14 \\
\end{bmatrix}

\begin{bmatrix}
	(2(1)+5(14)) \pmod{26} \\
	(3(1) + 11(14)) \pmod{26} \\
\end{bmatrix}

\equiv

\begin{bmatrix}
	20 \\
	1 \\
\end{bmatrix}

\rightarrow \texttt{"UB"}
$$
$$


\texttt{"ok"} \rightarrow 
\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix}

\rightarrow

\begin{bmatrix}
	2 & 5 \\
	3 & 11 \\
\end{bmatrix}

\times

\begin{bmatrix}
	14 \\
	10 \\
\end{bmatrix}

\begin{bmatrix}
	(2(14)+5(10)) \pmod{26} \\
	(3(14) + 11(10)) \pmod{26} \\
\end{bmatrix}

\equiv

\begin{bmatrix}
	0 \\
	22 \\
\end{bmatrix}

\rightarrow \texttt{"AW"}
$$
$$E(\texttt{"book"}) \rightarrow \texttt{"UBAW"}$$

## Question 2

For $2 \times 2$ Matrix, $\begin{bmatrix} a & b \\ c & d \end{bmatrix}$, the determinant is $ad-bc$
and the adjugate is $\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$


Matrix $A$ = $\begin{bmatrix} 2 & 3 \\ 9 & 7 \end{bmatrix}$
Determinant of $A \equiv (2 \cdot 7) - (9 \cdot 3) \equiv 14 - 27 \equiv -13 \pmod{26}$ 
$-13$ does not have a multiplicative inverse, so $A$ is not a valid key matrix

Matrix $B$ = $\begin{bmatrix} 5 & 7 \\ 2 & 3 \end{bmatrix}$
Determinant of $A \equiv (5 \cdot 3) - (7 \cdot 2) \equiv 15 - 14 \equiv 1 \pmod{26}$ 
Inverse of $1 \equiv 1$ because $1 \times 1 \equiv 1 \pmod{26}$
Inverse of $B \pmod{26}$:

$$
B^{-1} \equiv
\frac{1}{\texttt{det}(B)}  \times
\begin{bmatrix}3 & -7 \\ -2 & 5 \end{bmatrix} \equiv
1  \times
\begin{bmatrix}3 & -7 \\ -2 & 5 \end{bmatrix} \equiv
\begin{bmatrix}3 & -7 \\ -2 & 5 \end{bmatrix} \equiv
\begin{bmatrix}3 & 19 \\ 24 & 5 \end{bmatrix} \pmod{26}
$$

Matrix $C$ = $\begin{bmatrix} 2 & 4 \\ 3 & 6 \end{bmatrix}$
Determinant of $B \equiv (2 \cdot 6) - (3 \cdot 4) \equiv 12 - 12 \equiv 0 \pmod{26}$ 
$0$ does not have a multiplicative inverse, so $C$ is not a valid key matrix

Matrix $D$ = $\begin{bmatrix} 5 & 11 \\ 1 & 4 \end{bmatrix}$
Determinant of $D \equiv (5 \cdot 4) - (1 \cdot 11) \equiv 20 - 11 \equiv 9 \pmod{26}$ 
Inverse of $9 \equiv 3$ because $9 \times 3 \equiv 27 \equiv 1 \pmod{26}$
Inverse of $B \pmod{26}$:

$$
D^{-1} \equiv
\frac{1}{\texttt{det}(D)}  \times
\begin{bmatrix}4 & -11 \\ -1 & 5 \end{bmatrix} \equiv
3  \times
\begin{bmatrix}4 & -11 \\ -1 & 5 \end{bmatrix} \equiv
\begin{bmatrix}12 & 19 \\ 23 & 15 \end{bmatrix} \pmod{26}
$$

## Question 3

The ciphertext $\texttt{ELNI}$ was encrypted by a Hill cipher with a $2 \times 2$ matrix. The plaintext is $\texttt{dont}$. Find the encryption matrix $M$.

$\texttt{"dont"} \rightarrow D = 3, O = 14, N = 13, T = 19$
$\texttt{"ELNI"} \rightarrow E = 4, L = 11, N = 13, I = 8$

Plaintext vectors: $P_1 = \begin{bmatrix} 3 \\ 14 \end{bmatrix}$, and $P_2 = \begin{bmatrix} 13 \\ 19 \end{bmatrix}$

Ciphertext vectors: $C_1 = \begin{bmatrix} 4 \\ 11 \end{bmatrix}$, and $C_2 = \begin{bmatrix} 13 \\ 8 \end{bmatrix}$

Hill Cipher encryption is represented by $C \equiv MP \pmod{26}$

$P_1 = M \cdot C_1$
$\begin{bmatrix} 4 \\ 11 \end{bmatrix} = M \cdot \begin{bmatrix} 3 \\ 14 \end{bmatrix}$


$P_2 = M \cdot C_2$
$\begin{bmatrix} 13 \\ 8 \end{bmatrix} = M \cdot  \begin{bmatrix} 13 \\ 19 \end{bmatrix}$

To solve for $M$, the encryption matrix can be found by $M \equiv C P^{-1}$

$$
M = \begin{bmatrix} 4 & 13 \\ 11 & 8 \end{bmatrix}
\left (
\begin{bmatrix} 4 & 13 \\ 11 & 8 \end{bmatrix}
\right ) ^{-1}
$$

$$
P^{-1} \equiv \left( \begin{bmatrix} 3 & 13 \\ 14 & 19 \end{bmatrix} \right)^{-1} \pmod{26} 
$$

$$
\text{det}(P) = (3 \times 19) - (13 \times 14) = 57 - 182 = -125 \pmod{26} 
$$

$$
\text{det}(P)^{-1} \pmod{26} = \text{(modular inverse of -125 modulo 26)}
$$
$$ -125 \equiv 5 \pmod{26}$$


$$
5 \times x \equiv 1 \pmod{26} \Rightarrow x = 21
$$

$$
P^{-1} \equiv 21 \times \begin{bmatrix} 19 & -13 \\ -14 & 3 \end{bmatrix} \pmod{26}
$$

$$
P^{-1} \equiv \begin{bmatrix} 19 \cdot 21 & -13 \cdot 21 \\ -14 \cdot 21 & 3 \cdot 21 \end{bmatrix} \pmod{26}
$$

$$
P^{-1} \equiv \begin{bmatrix} 399 & -273 \\ -294 & 63 \end{bmatrix} \pmod{26}
$$

$$
P^{-1} \equiv \begin{bmatrix} 15 & 7 \\ 20 & 11 \end{bmatrix} \pmod{26}
$$

$$
M = \begin{bmatrix} 4 & 13 \\ 11 & 8 \end{bmatrix} \times \begin{bmatrix} 15 & 7 \\ 20 & 11 \end{bmatrix} \equiv \begin{bmatrix} 10 & 13 \\ 9 & 23 \end{bmatrix} \pmod{26}
$$

## Question 4

Let $c,d,e,f,g,h$ be integers $\pmod{26}$.  Consider the following combination of the Hill and affine ciphers: represent a block of plaintext as a pair $(x,y) \pmod{26}$.  The corresponding ciphertext $(u,v)$ is 
$$(x,y)
\left(
\begin{array}{ll} c&d \\ e&f\\ \end{array}
\right)+
(g,h) \equiv
(v,w) \pmod{26}
$$  
Encrypt the plaintext $\texttt{here}$ using the values below:
$$(x,y)
\left(
\begin{array}{ll} 3&4 \\ 3&1 \\
\end{array}
\right) + 
(8,11) \equiv 
(v,w) \pmod{26}
$$  
### Answer part A
$$
h = 7,
e = 4,
r = 17,
e = 4,
$$

$$
\texttt{here} \rightarrow \begin{bmatrix} 7 \\ 4\end{bmatrix} \text{, and } 
\begin{bmatrix} 17 \\ 4\end{bmatrix}
$$

$$
\begin{bmatrix}
7 \\ 4
\end{bmatrix}
\begin{bmatrix}
3 & 4 \\ 3 & 1
\end{bmatrix} +
\begin{bmatrix}
8 \\ 1
\end{bmatrix}
\equiv 
\begin{bmatrix}
v \\ w
\end{bmatrix}
\equiv
\begin{bmatrix}
19 \\ 10
\end{bmatrix}
\pmod{26}
$$
$$
\begin{bmatrix}
17 \\ 4
\end{bmatrix}
\begin{bmatrix}
3 & 4 \\ 3 & 1
\end{bmatrix} +
\begin{bmatrix}
8 \\ 1
\end{bmatrix}
\equiv 
\begin{bmatrix}
v \\ w
\end{bmatrix}
\equiv
\begin{bmatrix}
23 \\ 14
\end{bmatrix}
\pmod{26}
$$
$\begin{bmatrix} 19 \\ 10 \end{bmatrix} \rightarrow \begin{bmatrix} T \\ K \end{bmatrix}$

$\begin{bmatrix} 23 \\ 14 \end{bmatrix} \rightarrow \begin{bmatrix} X \\ O \end{bmatrix}$

So "here" becomes "TKXO"

### Answer part B

To perform a chosen plaintext attack on a system combining the Hill and affine ciphers, aiming to discover the key components $(c, d, e, f, g, h)$, follow these steps:

1. **Choose Plaintexts:**
   - First Block: Choose $(x_1, y_1) = (0, 1)$, simplifying to the vector $[0, 1]$.
   - Second Block: Choose $(x_2, y_2) = (1, 0)$, simplifying to the vector $[1, 0]$.

2. **Encrypt the Chosen Plaintexts:**
   - Encrypting $[0, 1]$ reveals $(d + g, f + h) \pmod{26}$.
   - Encrypting $[1, 0]$ reveals $(c + g, e + h) \pmod{26}$.

3. **Recover the Key:**
   - The outputs from encrypting these blocks directly relate to the components of the encryption matrix and the additive component.
   - Solve for $c, d, e, f$ by isolating these values using the known outputs and subtracting the values of $g$ and $h$.

This method leverages the simplicity of choosing plaintexts that effectively mimic the identity matrix's impact on the encryption process, thus simplifying the extraction of the encryption matrix and additive component from the observed ciphertexts.



## Question 5

Use Euclid's Algorithm to find integers $x$ and $y$ so that $$79x+31y =1$$
Use this to determine $31^{-1} \pmod{79}$. (Give your answer as a number between 0 and 78.)

![[Extended Euclid Python v2]]












