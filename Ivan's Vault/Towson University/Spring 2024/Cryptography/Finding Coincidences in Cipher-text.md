---
tags:
  - MATH-314
---

To detect the length of the key in a [[Vigenère Cipher]] using cipher-text only, one method involves shifting the cipher-text against itself and counting the coincidences. This helps in estimating the key length. 

### Example

Suppose we have a cipher-text: `EEBQAARLM`

- **Original Cipher-text**: EEBQAARLM
- **Shift by 1**: \_EEBQAARLM
- **Shift by 2**: \_\_EEBQAARLM
- **Shift by 3**: \_\_\_EEBQAARLM

And so on. For each shift, align the letters and count how many times the same letter appears in the same position in the original and the shifted string.

### Coincidence Counting

- **Shift 1**: No coincidences.
- **Shift 2**: No coincidences.
- **Shift 3**: 1 coincidence (the letter 'B').

This method is repeated for multiple shifts. A higher number of coincidences at a specific shift distance can indicate that the shift distance is a multiple of the key length. This is because the same key letters would be aligning with the same plaintext letters, leading to repeated patterns in the cipher-text.

