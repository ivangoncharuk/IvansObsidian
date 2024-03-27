#fall2023 #COSC-455 

## The Basics

The Pumping Lemma is **a tool used to prove that a given language is not regular**. 
It says that for any regular language $L$, there exists a constant $p$ (the "pumping length") such that any string $s$ in $L$ with length at least $p$ can be divided into three parts $s = xyz$, satisfying:

1. $xy^i z$ is in $L$ for all $i \geq 0$.
2. $|y| > 0$ (i.e., $y$ is not empty).
3. $|xy| \leq p$.

If you find a string $s$ in $L$ that violates any of these conditions, then $L$ is not a regular language.

### Examples

#### Example 1: $L = \{ a^n b^n | n \geq 1 \}$

1. Choose a string $s = a^p b^p$ where $p$ is the pumping length.
2. Try to divide $s$ into $xyz$ to satisfy the conditions.
3. You'll find that no matter how you divide it, you can't satisfy all three conditions.
4. Conclusion: $L$ is not a regular language.

#### Example 2: $L = \{ a^n | n \geq 0 \}$

1. Choose a string $s = a^p$ where $p$ is the pumping length.
2. Divide $s = xyz = a^{p-1} a^1$ where $x = a^{p-1}$, $y = a^1$, $z = \epsilon$.
3. All conditions are met:
   - $xy^i z = a^{p-1} a^i$ is in $L$ for all $i \geq 0$.
   - $|y| = 1 > 0$.
   - $|xy| = p \leq p$.
4. Conclusion: $L$ could be a regular language (Pumping Lemma is not violated).

The Pumping Lemma is mainly used for proving non-regularity. If a language satisfies the Pumping Lemma, it doesn't necessarily mean it's regular; it just means it hasn't been proven non-regular by this method.