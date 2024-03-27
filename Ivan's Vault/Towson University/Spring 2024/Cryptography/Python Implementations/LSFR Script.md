---
tags:
  - MATH-314
  - spring2024
---

```python
def lfsr_crypt(data: bytes, seed: int, polynomial: int, length: int) -> bytes:
    """
    Encrypts or decrypts data using an LFSR-generated keystream.

    Args:
        data (bytes): The input data to encrypt or decrypt.
        seed (int): The initial seed value for the LFSR.
        polynomial (int): The feedback polynomial for the LFSR.
        length (int): The length of the LFSR register in bits.

    Returns:
        bytes: The encrypted or decrypted data.
    """
    register = seed
    result = bytearray()
    mask = (1 << length) - 1  # Mask to ensure register stays within length

    for byte in data:
        key_byte = 0
        for _ in range(8):  # Generate 8 bits for the keystream byte
            lsb = register & 1
            register = (register >> 1) | ((bin(register & polynomial).count('1') % 2) << (length - 1))
            register &= mask
            key_byte = (key_byte >> 1) | (lsb << 7)
        
        result.append(key_byte ^ byte)
    
    return bytes(result)

# Example usage
data = b"hello world"  # Data to encrypt
seed = 0x12345678  # Initial seed for the LFSR
polynomial = 0x87654321  # Feedback polynomial
length = 32  # Length of the LFSR register in bits

encrypted_data = lfsr_crypt(data, seed, polynomial, length)
print("Encrypted data:", encrypted_data)

# Decrypting the data (since encryption is reversible)
decrypted_data = lfsr_crypt(encrypted_data, seed, polynomial, length)
print("Decrypted data:", decrypted_data)
```






