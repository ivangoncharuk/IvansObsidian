#job #ciphertech 


## Code 
![[Challenge 1 Solution]]

### Variables
- `F`: This is the feedback value for the Linear Feedback Shift Register (LFSR), initialized to `0x87654321` as per the specification.
- `S`: This is the initial value or state for the LFSR, passed as a parameter to the function.
- `result`: A `bytearray` to store the final result.

### Explanation 
1. For each byte in the input data, the LFSR (`S`) is stepped 8 times.
2. If the lowest bit of `S` is 1, `S` is shifted right by 1 (equivalent to integer division by 2) and XORed with `F`.
3. If the lowest bit of `S` is 0, `S` is simply shifted right by 1.
  
  > This stepping generates a pseudo-random key sequence that is more robust than simply XORing with a static key.

1. After the LFSR has been stepped 8 times, we extract the lowest byte from `S` using the bitwise **AND** operation `S & 0xFF`.
2. Each byte of the data is then XORed with this lowest byte (`key_byte`) to produce a new byte. The new byte is then appended to the `result`.

Finally, the function returns `result` as a `bytes` object, converting from the `bytearray`.

- The function is symmetric, meaning you can use it for both encryption and decryption. 
- The encrypted data can be decrypted back using the same initial value for the LFSR.
> Not highly secure by modern standards, but it is a good example of how encryption and LFSR works.

---

## Research Content

![Research Video](https://www.youtube.com/watch?v=Ks1pw1X22y4)

![Cryptography: LFSR by NC School of Science and Math](https://www.youtube.com/watch?v=1UCaZjdRC_c)

[Linear-feedback shift register (Wikipedia)](https://en.wikipedia.org/wiki/Linear-feedback_shift_register)

