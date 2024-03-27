#job #ciphertech 


**From $\rightarrow$ [[2018 Challenge Instructions 1.pdf]]**

![[Cipher Challenge 2 Original Prompt]]


### What the Challenge is Asking You To Do

In this challenge, I am asked to read a custom file format with the extension `.KDB` and extract the data stored within it. The contents of the KDB file are encrypted using an LFSR algorithm (which is the same one as in Challenge 1), so I will need to decode the extracted data using this algorithm.

My program should:

1. Accept a path to a `.KDB` file as a command-line argument.
2. Read and parse the file according to the given file specification.
3. Decrypt the extracted information using the LFSR algorithm.
4. Output the extracted and decoded information to standard output, one entry per line.

### File Specification

- The file starts with a header (`HEAD`) containing the following fields:
    - `MAGIC`: A 6-byte string `"CT2018"`
    - `ENTRY_LIST`: A 4-byte little-endian integer that is a pointer to the `ENTRY_LIST` structure.

- `ENTRY_LIST`: An array of up to 127 `ENTRY` structures. 
  - It ends when the value `0xFFFFFFFF` is encountered.

- `ENTRY`: Contains an ASCII-encoded, null-terminated name and a pointer to the `BLOCK_LIST` structure for that entry.

- `BLOCK_LIST`: Contains an array of up to 255 `BLOCK` structures.
 
- `BLOCK`: Contains a 2-byte little-endian integer (`SIZE`) that specifies the size of the block's data and a 4-byte little-endian integer (`DATA`) that is a pointer to the actual data.

- `DATA`: A byte array that is encoded using the LFSR algorithm.

All pointers are relative to the beginning of the file, and the initial value for the LFSR algorithm is given as `0x4F574154`.

---
### Solution

1. The ENTRY name is a null-terminated string but occupies 16 bytes space.
2. We need to handle the condition where the value of 0xFFFFFFFF signifies the end of ENTRY_LIST.
3. We have to concatenate all BLOCKS from an ENTRY before decoding them.

