---
tags:
  - MATH-314
  - spring2024
---

```python
def encrypt_affine_cipher(plaintext, a, b, mod=26):
    """
    Encrypts plaintext using an affine cipher.
    
    Parameters:
    - plaintext: The input string to encrypt.
    - a: The multiplicative part of the affine cipher.
    - b: The additive part of the affine cipher.
    - mod: The modulus, representing the size of the alphabet (26 for the English alphabet).
    
    Returns:
    The encrypted text as a string.
    """
    encrypted_text = ""  # Initialize the encrypted text as an empty string
    for char in plaintext:
        if char.isalpha():  # Ensure the character is a letter
            # Convert the character to a number (0-25), where A=0, B=1, ..., Z=25
            x = ord(char.upper()) - ord('A')
            # Apply the affine cipher formula: E(x) = (a*x + b) mod 26
            E_x = (a * x + b) % mod
            # Convert the number back to a letter and add it to the encrypted text
            encrypted_char = chr(E_x + ord('A'))
            encrypted_text += encrypted_char
        else:
            # Directly add non-alphabet characters to the encrypted text without modification
            encrypted_text += char
    return encrypted_text

# Encryption parameters
a = 17  # Multiplicative component
b = 7   # Additive component

# Plaintext message to encrypt
plaintext = "letters"

# Perform encryption
encrypted_text = encrypt_affine_cipher(plaintext, a, b)


print(f"'{plaintext}' encrypts to: '{encrypted_text}'")

```