```python
def Crypt(data: bytes, initialValue: int) -> bytes:
	# Initialize feedback (F) and state (S) for the LFSR
	F = 0x87654321
	S = initialValue
	result = bytearray()
	for byte in data:
		# Step the LFSR 8 times to generate the key
		for _ in range(8):
			if S & 1: # Check the lowest bit for LFSR feedback
				S = (S >> 1) ^ F # Shift right and XOR with F
			else:
				S = S >> 1 # Shift right if the lowest bit is 0
		key_byte = S & 0xFF
		result.append(key_byte ^ byte)
	return bytes(result) # Return the result as bytes

encrypted_apple = str(Crypt(b"apple", 0x12345678))
print("Encrypting b'apple': ", encrypted_apple)
print(
	"Decrypting",
	encrypted_apple,
	str(Crypt(b"\xCD\x01\xEF\xD7\x30", 0x12345678)),
)
```

#ciphertech 