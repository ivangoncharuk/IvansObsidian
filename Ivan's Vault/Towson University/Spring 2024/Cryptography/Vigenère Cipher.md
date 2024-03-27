---
tags:
  - spring2024
  - "#MATH-314"
---


- Select a keyword.
- Encrypt by converting plaintext to numbers; below it, write the key converted to numbers.
- Add the two rows modulo 26.

### Example

Plaintext: "car" -> 2 0 17  
Keyword: "students" -> 18 19 20 3 4 13 19 18  
Resulting cipher text: "UTLFEEVS"

### Decryption

- Subtract the key from the ciphertext.

### Known Plaintext Attack

- Subtract the plaintext from the ciphertext to find the key.

### Ciphertext Only

- More challenging due to the difficulty in determining the key length.
- Shift the ciphertext and count coincidences to estimate the key length.
