#ciphertech 
> A common technique for obfuscating data is to use exclusive-or (XOR) with some key; it is inexpensive and symmetric. A problem occurs when this is used on file formats like portable executable where there are many null bytes, since XORing nulls with the key ends up writing the key out.
> 
> A slightly more complex algorithm uses a Linear Feedback Shift Register (LFS) to produce a key stream, which will be XORed with the data. A generic LFSR is:
> 
> IF `F` is the value which represents the LFSR feedback and `S` is the current state of the LFS, the next state of the LFSR is computed as follows:
	if the lowest bit of `S` is 0: `S` = `S` >> 1 if the lowest bit of `S` is 1: `S` = (5 >> 1) ^ F
	
- For this challenge, you'll be using an LFS with the feedback value `0x87654321`. The LFS is initialized with a value and stepped to produce the key stream.
- The next key value is read from the LFSR after eight steps, with the actual key being the lowest byte of the current LFSR value.

- For example, if the initial value of the LFSR is `OxFFFFFFFF`, then next value after stepping it eight times will be `9x9243F425`, meaning that the first key byte is `0x25`. If the first byte of the input is `0x41`, the first byte of output will be `0×64`.

- Your task is to implement this algorithm (both LFS and the XOR). We're only interested in algorithm implementation; other code will be discarded.

- The function should adhere to one of following signatures:
```Python
Crypt(data: bytes, initialValue: int) -> bytes
```

```Java
static byte[] Crypt(byte[] data, long initialValue)
```

```csharp
static byte[] Crypt(byte[] data, uint initialValue)
```

```cpp
unsigned char *Crypt(unsigned char *data, int datalength, unsigned int initialValue)
```

Example Tests:

data: `"apple"`
dataLength: `5`
initialValue: `0x12345678`
result: `"\xCD\x01\xEF\xD7\x30"`

data: `"\xCD\x01\xEF\xD7\x30"`
dataLength: `5`
initialValue: `0x12345678`
result: `"apple"`

![[Challenge 1 Solution]]

This is how the [[Linear Feedback Shift Register]] works.