
Homework due tonight! :(

Review for exam

- Few mins on first question (SAES encryption)
### How do affine cipher and shift cipher work (notes)


## Extended Euclid

Find $13^{-1} \pmod{ 44}$

1. gcd(forward)
	1. gcd(44, 13)
		1. 44 = 3(13) + `5` (remainder)
		2. 13 = 2(5) + 3
		3. 5 = 1(3) + 2
		4. 3 = 1(2) + 1 gcd
		5. (we get 0 at this step)
	2. work backwards pt a
		1. `5` = 44 - **3**(*13*)
		2. **3** = *13* - **2**(*5*)
		3. **2** = *5* - **1**(*3*)
		4. **1** = *3* - 1(2)
	3. work backwards pt b
		1. 1 = 3 - 1 (*5* - **1**(*3*)) because **2** = *5* - **1**(*3*)
		2. 1 = *3* - 5 + *3*
		3. 1 = 2(*3*) - 5
		4. 1 = 2(*13* - **2**(*5*)) - 5 because **3** = *13* - **2**(*5*)
		5. 1 = 2(13) - 2(5) - 5
		6. 1 = 2(13) - 4(5) $\cancel{-5}$
		8. 1 = 2(13) - 5(`5`)
		9. 1 = 2(13) - 5`(`44 - **3**(*13*)`)` because `5` = 44 - **3**(*13*)
		10. 1 = 2(13) - 5(44) - 15(13)
		11. 1 = 17(13) $\cancel{- 5(44)}$ because we are in $\pmod{44}$
		12. $1 \equiv 17(13) \pmod{44}$



In F16 (mod x^4 + x + 1), multiply (x^2 + x)(x^3 + 1)

(x^2 + x)(x^3 + 1)
(x^5 + x^2) + x^4 + x
\= x^5 + x^4 + x^2 + x

take this inside a quotation thingy and x^4 + x + 1 on the outside because of the mod

multiply $\rightarrow (x^2 + x)(x^3 + 1) \equiv x + 1$


## Convert TEXT to Ciphertext using key

TEXT ->
19 4 23 19
8 19 8 19 =
\----------
27 2 31 38
1 23 5 12 (mod 26)
cipher text BXFM

$17(13)x \equiv 3(17) \pmod{44}$




