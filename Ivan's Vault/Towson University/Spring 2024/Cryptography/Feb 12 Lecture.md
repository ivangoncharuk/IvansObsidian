---
tags:
  - MATH-314
  - spring2024
---
# Cipher-text Only Attack (Hill Cipher)

## Frequency Analysis on Blocks
- For block sizes of 2 or 3, frequency analysis on blocks can be applied.
- Identify the most frequently occurring blocks.
- It's common to guess that these correspond to one of the most frequent bigrams (for block size 2) or trigrams (for block size 3).
  - **Most Frequent Bigram:** `'th'`
  - **Second Most Frequent Bigrams:** There's a tie between `'er'` and `'he'`.

## Moving Beyond mod(26)

### Residue Modulo n
- A residue modulo $n$ represents all integers that yield the same remainder when divided by $n$.
- Typically, residues are represented by remainders ranging from 0 to $n-1$.
- Example: The residue $5 \pmod{26}$ includes numbers such as $\{-3, 5, 1, 3, 21, 28, \dots\}$.

### Notation for Set of All Residues
- The notation $\mathbb{Z}_m$ is used for the set of all residues modulo \(m\).
  - For instance, $\mathbb{Z}_6 = \{0, 1, 3, 4, 5\}$.

### Ring Properties
- $\mathbb{Z}_m$ is considered a **ring**, which means:
  - We can perform addition, subtraction, and multiplication on residues.
  - Any representative of a residue class can be used for arithmetic operations.
  - A collection that allows for these operations, adhering to regular arithmetic rules, is termed a ring.

### Division and Inverses
- Ideally, division is performed by finding inverses.
  - **Fact:** $a \pmod{m}$ has an inverse $a^{-1}$ (such that $a \cdot a^{-1} \equiv 1 \mod{m}$) if and only if $\gcd(a, m) = 1$.

## Idea: Euclid's Algorithm

### Computing GCDs Quickly

- To compute the greatest common divisor (gcd) of two numbers quickly, consider gcd(45, 50).

#### One Way: Factor Both Numbers

- **Fact 1:** We can perform division with remainder (long division) of $a$ by $b$ to always get a remainder $r$ smaller than $b$:
  $a = bq + r$
  $0 \leq r < b$

- **Fact 2:** If $d$ divides $a$ and $b$, then $d$ divides $a - bq = r$:
  - Thus, $d$ divides $r$.
  - Similarly, any $d$ that divides both $b$ and $r$ divides $qb + r = a$.

#### Iterative Process

- Putting these observations together, we see that $gcd(a,b) = gcd(b, r)$.
- This process can be iterated: each time, the numbers get smaller.
- Once a remainder of 0 is obtained, the previous remainder is the gcd.

### Example

#### Computing gcd(119, 91)

##### Initial Setup

- We aim to find the greatest common divisor (gcd) of 119 and 91.

##### Application of Euclid's Algorithm

- **Step 1:** Divide 119 by 91:
  $119 = 91 \times 1 + 28$
  - Here, $a = 119$, $b = 91$, and $r = 28$.

- **Fact:** If $d$ divides both $a$ and $b$, then it also divides $a - bq = r$.

#### Iterative Process

- **Step 2:** Now, apply the algorithm with $b = 91$ and the new remainder $r = 28$:
  $91 = 28 \times 3 + 7$
  - The new remainder $r$ is 7.

- **Step 3:** Continue with $b = 28$ and $r = 7$:
  $28 = 7 \times 4 + 0$
  - The remainder is now 0, so we stop.

#### Conclusion

- The previous remainder before obtaining 0 is 7, which is the gcd of 119 and 91.
- Therefore, $gcd(119, 91) = 7$.


### Python Implementation

![[Euclid Python Implementation]]

## Extended Euclid's Algorithm

### Finding Integers $x$ and $y$ for $gcd(a,b) = d$

- Given $gcd(a,b) = d$, there exist integers $x$ and $y$ such that $ax + by = d$.
- By working backward with Euclid's Algorithm, we can determine $x$ and $y$.

#### Writing Down Equations with Remainder

- $119 = 1(91) + 28 \Rightarrow 28 = 119 - 1(91)$
- $91 = 3(28) + 7 \Rightarrow 7 = 91 - 3(28)$

#### Solving for the Remainder

- Start by solving each equation for the remainder.

#### Substituting Equations Repeatedly

- Then, repeatedly substitute the remainder equation into the previous one.

#### Final Distribution of Coefficients

- After substitution and distribution, we get:
  - $7 = 91 - 3(119 - 1(91))$
  - $= 91 - 3(119) + 3(91)$

#### Conclusion

- This leads to the final equation showing the relationship:
  - $7 = 4(91) - 3(119)$

### Finding $x$ and $y$ for $11x + 52y = 1$ Using Euclid's Algorithm

### Goal
- To find integers $x$ and $y$ such that $11x + 52y = 1$.

### Applying Euclid's Algorithm
1. First, we find the gcd of 11 and 52, which is crucial for ensuring that $11x + 52y = 1$ can be solved (since gcd(11, 52) = 1, a solution exists).

2. Start with the division: $52 = 11 \times 4 + 8$
   - This implies $8 = 52 - 11 \times 4$.

3. Next, divide 11 by 8: $11 = 8 \times 1 + 3$
   - This implies $3 = 11 - 8 \times 1$.

4. Then, divide 8 by 3: $8 = 3 \times 2 + 2$
   - This implies $2 = 8 - 3 \times 2$.

5. Finally, divide 3 by 2: $3 = 2 \times 1 + 1$
   - This implies $1 = 3 - 2 \times 1$.

### Working Backwards to Find $x$ and $y$
1. Substitute $2 = 8 - 3 \times 2$ into $1 = 3 - 2 \times 1$:
   - $1 = 3 - (8 - 3 \times 2) \times 1$
   - $= 3 \times 3 - 8$.

2. Substitute $3 = 11 - 8 \times 1$:
   - $1 = (11 - 8) \times 3 - 8$
   - $= 11 \times 3 - 8 \times 4$.

3. Substitute $8 = 52 - 11 \times 4$:
   - $1 = 11 \times 3 - (52 - 11 \times 4) \times 4$
   - $= 11 \times 3 - 52 \times 4 + 11 \times 16$
   - $= 11 \times 19 - 52 \times 4$.

### Conclusion
- Therefore, $x = 19$ and $y = -4$ are the integers that satisfy $11x + 52y = 1$.


### Exented Euclid Python Implementation
![[Exented Euclid Python Implementation]]




