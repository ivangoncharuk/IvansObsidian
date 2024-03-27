---
tags:
  - MATH-314
  - spring2024
---

# Linear Feedback Shift Register (LFSR)

[[Linear Feedback Shift Register]] (LFSR) is a mechanism for generating a sequence of binary digits. The core principle behind an LFSR is relatively straightforward: it shifts bits through a register, with the new bit entering the register being a linear function (usually XOR) of certain bits within the register, known as "taps". LFSRs are widely used in fields such as cryptography for generating pseudo-random sequences and in digital circuits for test pattern generation.

## How LFSR Works

An LFSR operates by shifting bits to the right or left, with the vacated bit being recalculated as a function of the bits at the tap positions. The steps for generating a sequence are as follows:

1. **Initialization**: Load the LFSR with an initial value, which is called the seed. It's crucial that the seed is not all zeros.
2. **Shift Operation**: Shift the register by one position. This could be either to the left or to the right.
3. **Feedback Calculation**: Calculate the new bit (the one entering the vacated position) by performing an XOR operation on the bits at the specified tap positions.
4. **Repeat**: The shift and feedback calculation are repeated to generate a sequence of bits.

### Example

Consider a 4-bit LFSR with taps at positions 2 and 4 (counting from the right, starting with 1). The feedback function is the XOR of the bits at these positions.

| Step | Register State | New Bit (XOR of Taps) |
|------|----------------|-----------------------|
| 0    | 1001           | -                     |
| 1    | 1100           | 1 (1 XOR 0)           |
| 2    | 0110           | 0 (0 XOR 0)           |
| 3    | 0011           | 1 (1 XOR 1)           |
| ...  | ...            | ...                   |

This process repeats, generating a pseudo-random sequence of bits. The sequence's period depends on the taps' positions and the initial seed.

## Python Script for LFSR

Below is a simple Python script that implements an LFSR with customizable length, seed, and tap positions.

![[LSFR Script]]


$$
S_{m+j} \equiv p_{m-1}S_{m+j-1} + p_{m-2}S_{m+j-2} + \cdots + p_0S_j \pmod{2}
$$

Based on the given pattern for generating new bits, the sequence up to $S_9$ is as follows:

- $S_0 = 1$
- $S_1 = 1$
- $S_2 = 0$
- $S_3 = 0$
- $S_4 = 0$ calculated as $S_4 \equiv S_3 + S_1 + S_0 \pmod{2} \rightarrow 0 + 1 + 1 \equiv 0 \pmod{2}$
- $S_5 = 1$ calculated as $S_5 \equiv S_4 + S_2 + S_1 \pmod{2} \rightarrow 0 + 0 + 1 \equiv 1 \pmod{2}$
- $S_6 = 1$ calculated as $S_6 \equiv S_5 + S_3 + S_2 \pmod{2} \rightarrow 1 + 0 + 0 \equiv 1 \pmod{2}$
- $S_7 = 1$ calculated as $S_7 \equiv S_6 + S_4 + S_3 \pmod{2} \rightarrow 1 + 0 + 0 \equiv 1 \pmod{2}$
- $S_8 = 0$ calculated as $S_8 \equiv S_7 + S_5 + S_4 \pmod{2} \rightarrow 1 + 1 + 0 \equiv 0 \pmod{2}$
- $S_9 = 0$ calculated as $S_9 \equiv S_8 + S_6 + S_5 \pmod{2} \rightarrow 0 + 1 + 1 \equiv 0 \pmod{2}$



This process involves using the formula $S_{m+j} \equiv p_{m-1}S_{m+j-1} + p_{m-2}S_{m+j-2} + \cdots + p_0S_j \pmod{2}$, which, for our specific example, simplified to using the bits $S_{i-1}$, $S_{i-3}$, and $S_{i-4}$ to calculate $S_i$. Each new bit is the sum of these selected previous bits modulo 2, following the pattern of feedback coefficients defined implicitly by our initial calculation and assumptions.

The sequence of bits represents the pseudorandom output of the LFSR based on the initial seed and the specific feedback mechanism defined. To determine the period of this sequence, we would look for when the sequence of bits repeats itself. Given the calculated bits up to $S_9$, we do not yet see a complete repetition starting from the initial seed, so more steps would be required to fully determine the period. However, the maximum period of an LFSR sequence can be $2^m - 1$ where $m$ is the number of bits in the register, assuming the LFSR is maximally periodic. In this case, as we have not completed enough steps to see the sequence repeat, we cannot definitively state the period without further calculation.

Example:

$m=3$, $p_0 = 1$, $p_1 = 0$, $p_2 = 1$, and initial seed values are $s_0​=1$, $s_1​=1$, $s_2​=1$, let's use a table to track the state of the LFSR and the generated bits until we observe a repetition. This will help us calculate the period of the sequence.

| Step | State (Before) | Generated Bit | State (After) | Note                |
|------|----------------|---------------|---------------|---------------------|
| 1    | 111            | -             | 111           | Initial state       |
| 2    | 111            | 0             | 110           | S_3 = S_0 + S_2 mod 2 |
| 3    | 110            | 1             | 101           | S_4 = S_1 + S_3 mod 2 |
| 4    | 101            | 0             | 010           | S_5 = S_2 + S_4 mod 2 |
| 5    | 010            | 0             | 001           | S_6 = S_3 + S_5 mod 2 |
| 6    | 001            | 1             | 100           | S_7 = S_4 + S_6 mod 2 |
| 7    | 100            | 1             | 110           | S_8 = S_5 + S_7 mod 2 |
| 8    | 110            | 1             | 111           | S_9 = S_6 + S_8 mod 2 |
| 9    | 111            | 0             | 110           | Repeat of Step 2    |

In this example, the sequence of bits generated is as follows: `0, 1, 0, 0, 1, 1, 1, 0`. 

At step 9, the state of the LFSR returns to `110`, which is the same state we observed at step 2 after the initial generation began. This indicates that the sequence of states (and thus the generated bits) will repeat from this point forward.

The **period** of this LFSR sequence is **7**, as it cycles through 7 unique states before repeating. 
This is the *maximal period* for an LFSR of length 3, demonstrating that with a carefully chosen set of feedback coefficients and an appropriate initial seed, an LFSR can achieve a maximal period of $2^m-1$, where $m$ is the number of bits in the register.


The connection polynomial of an LFSR of degree m is
$$
C(x) = x^m + P_{m-1}x^{m-1} + P_{m-2}x^{m-2} + \dots + P_{1}x+P_0
$$
Ex: $m=4 \quad p_3=1, p_2 = 0, p_1 = 1, p_0 = 1$
$C(x) = x^4 + x^3 + x + 1$


If an LFSR has maximum degree, then its connection polynomial is irreducible

Bluetooth uses a cipher called **E0** which has 4 LSFRs with connection polynomials

- $x^{25} + x^{20} + x^{12} + x^{8} + 1$
- $x^{31} + x^{24} + x^{16} + x^{12} + 1$
- $x^{33} + x^{28} + x^{24} + x^{4} + 1$
- $x^{39} + x^{36} + x^{28} + x^{4} + 1$

Goes to blender? -> 1 bit of outpit -> used as key stream for stream cipher

What is the period of E0?