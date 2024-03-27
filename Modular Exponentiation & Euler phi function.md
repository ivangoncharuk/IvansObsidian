

Modular exponentiation is a type of exponentiation performed over a modulus. It is used in many areas of cryptography. This process is useful for large exponentiations, which could be impractical to compute directly due to the large sizes of numbers involved. Two main approaches to modular exponentiation are the direct method and the fast modular exponentiation method.

## Direct Method

The direct method of modular exponentiation involves computing the power $a^b$ directly and then taking the result modulo $n$. This is straightforward but can be very slow for large $b$, as it requires $b-1$ multiplications.

### Example: Compute $6^{74} \mod 11$ using the direct method

1. Multiply 6 by itself 73 times.
2. Take the result modulo 11.

This process is computationally intensive for large exponents and not practical for real-world applications.

#### Fast Modular Exponentiation

Fast modular exponentiation reduces the number of multiplications required by using the property that $a^{b} \mod n$ can be efficiently computed through repeated squaring. This method requires only $\log b$ multiplications.

##### Steps for Fast Modular Exponentiation:

1. Write $b$ in binary as a sum of powers of 2.
2. Repeatedly square $a \mod n$ until the exponent is as big as the biggest power of 2 in $b$.
3. Multiply together the powers of $a$ corresponding to the powers of 2 in $b$ and reduce $\mod n$.

##### Example: Compute $6^{74} \pmod{11}$ using fast modular exponentiation

1. **Write 74 in binary as a sum of powers of 2**: $74 = 64 + 8 + 2 = 2^6 + 2^3 + 2^1$. The binary representation of 74 is `1001010`.

2. **Repeated squaring starting with $6^1 \equiv 6 \mod 11$**:

    - Start with $6^1 \equiv 6 \mod 11$.
    - Square it to get $6^2 \equiv 36 \equiv 3 \mod 11$.
    - Continue squaring to build up to the largest power of 2 in the binary representation of 74.

3. **Multiply the necessary terms together**:

    - We calculate the required powers of 6 modulo 11, corresponding to $2^1$, $2^3$, and $2^6$ from the binary representation of 74.

4. **Reduce the final product modulo 11**:

Finally, the computation of $6^{74} \mod 11$ using the fast modular exponentiation method yields:

- Powers of 6 modulo 11 are: 
$6^1 \equiv 6$,
$6^2 \equiv 3$,
$6^4 \equiv 9$,
$6^8 \equiv 4$, 
$6^{16} \equiv 5$,
$6^{32} \equiv 3$, 
and $6^{64} \equiv 9$.
Thus, $6^{74} \mod 11 = 9$.

This demonstrates the efficiency of fast modular exponentiation, significantly reducing the computational effort from 73 multiplications to just $\log_2 74$ multiplications.

$6^{74} \equiv 6^{64+8+2}$
$\equiv (6^{64})\cdot (6^{8})\cdot (6^{2}) \pmod{11}$
$\equiv (9)\cdot (4)\cdot (3) \pmod{11}$
$\equiv 108 \equiv 9 \pmod{11}$

## What is the last digit of 7^35?
Compute $7^{35} \pmod{10}$

Write 35 as a sum of powers of 2 = 35 + 2 + 1

To compute the last digit of $7^{35}$, which is equivalent to $7^{35} \mod 10$, we use fast modular exponentiation:

1. **Binary representation**: $35$ in binary is $32 + 2 + 1 = 2^5 + 2^1 + 2^0$.

2. **Repeated squaring**:

   - $7^1 \equiv 7 \pmod{10}$
   - $7^2 \equiv 49 \equiv 9 \pmod{10}$
   - $7^4 = (7^2)^2 \equiv 9^2 = 81 \equiv 1 \pmod{10}$
   - Since $7^4 \equiv 1 \pmod{10}$, all higher powers of 4 (i.e., $7^8, 7^{16}, 7^{32}$) will also be congruent to $1 \pmod{10}$ due to the property of repeated squaring in modular arithmetic.

3. **Combine relevant powers**:

   Given $35 = 2^5 + 2^1 + 2^0$, we find the last digit by combining powers:

   - $7^{35} \equiv 7^{32} \times 7^2 \times 7^1 \equiv 1 \times 9 \times 7 \equiv 63 \pmod{10} \equiv 3 \pmod{10}$.

Therefore, the last digit of $7^{35}$ is $3$.

# Euler's $\varphi$ Function

Euler's $\varphi$ function, also known as Euler's totient function, is denoted as $\varphi(n)$. It counts the positive integers up to a given integer $n$ that are relatively prime to $n$. In simpler terms, it measures the number of integers less than $n$ which share no common divisors with $n$ other than $1$, or equivalently, the number of integers within the set $\{1, 2, ..., n\}$ that are coprime to $n$.

## Properties of Euler's $\varphi$ Function

1. **For a prime number $p$**: $\varphi(p) = p - 1$. This is because a prime number does not share any common divisors other than $1$ with any number less than itself.
   
2. **For two prime numbers $p$ and $q$**: If $n = pq$, then $\varphi(n) = (p-1)(q-1)$. This is due to the property that the product of two distinct prime numbers does not share any common divisors other than $1$ with numbers less than the product but greater than $1$.

3. **Multiplicative Property**: If two numbers $a$ and $b$ are coprime (i.e., $\gcd(a, b) = 1$), then $\varphi(ab) = \varphi(a) \cdot \varphi(b)$. This property is useful for calculating the totient of large numbers by breaking them down into their prime factorization.

## Application of Euler's $\varphi$ Function

One of the most significant applications of Euler's $\varphi$ function is in the field of cryptography, particularly in RSA encryption. It plays a crucial role in the generation of public and private keys. The function is also fundamental in number theory, especially in proving Euler's theorem and in the generalization of Fermat's little theorem.

## Example: Computing $\varphi(n)$

To compute $\varphi(n)$ for a given $n$, one approach is to factorize $n$ into its prime factors and then apply the properties of the $\varphi$ function. For instance:

- Given $n = 12$, its prime factorization is $2^2 \times 3$.
- Using the properties, we have $\varphi(12) = \varphi(2^2) \cdot \varphi(3) = (2^2 - 2^1) \cdot (3 - 1) = 2 \cdot 2 = 4$.

Thus, there are 4 integers that are coprime with 12, which are $1, 5, 7,$ and $11$





