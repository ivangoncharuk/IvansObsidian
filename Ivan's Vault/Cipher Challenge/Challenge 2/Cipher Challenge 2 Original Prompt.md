#ciphertech 
During a forensic investigation, a new data storage file format is discovered with the extension KDB. In addition to being stored in a custom format, the contents are encoded with the LFSR algorithm seen in Challenge 1, so all of the data contained in the file format must also be decoded once extracted. Using the provided spec on the next page, create a program that extracts and decodes the enclosed data.

- Your program should accept a path to a KDB file via command line argument. Your program should report the extracted, decoded information to standard out with each entry (name and stored information) on a separate line.
  
  Included is a sample KDB file named "store.kdb" The initial value for the LFSR algorithm is 0x4F574154

## KDB File Specification

| HEAD        |         |                           |
| ----------- | ------- | ------------------------- |
| MAGIC       | BYTE[6] | "CT2018"                  |
| ENTRY_LIST* | INT32   | Pointer to the ENTRY_LIST | 


| ENTRY_LIST |            |                  |
| ---------- | ---------- | ---------------- |
| ENTRIES    | ENTRY[127] | Array of ENTRIES | 


| ENTRY        |          |                           |
| ------------ | -------- | ------------------------- |
| NAME         | CHAR[16] | Null Terminated String    | 
| BLOCK_LIST * | INT32    | Pointer to the BLOCK_LIST |


| BLOCK_LIST |            |                 |
| ---------- | ---------- | --------------- |
| BLOCKS     | BLOCK[255] | Array of BLOCKS | 


| BLOCK |       |                             |
| ----- | ----- | --------------------------- |
| SIZE  | INT16 | Length of the BLOCK's data  |
| DATA* | INT32 | Pointer to the BLOCK's data | 


| DATA |        |                   |
| ---- | ------ | ----------------- |
| DATA | BYTE[] | An array of bytes | 

- All pointers are relative to the beginning of the file.
- The BLOCK's size and all pointers are little endian.
- All KDB files begin with a HEAD at 0x0, which starts with the magic bytes "CT2018" and contains a pointer to the file's ENTRY_LIST
- The ENTRY_LIST is an array of up to 127 ENTRIES. The value of 0xFFFFFFFF signified the end of ENTRY_LIST
- Each ENTRY has an ASCII encoded, null terminated name and a pointer to the ENTRY's BLOCK_LIST
- Each BLOCK contains a pointer to that BLOCK's DATA and the size of that DATA
- The DATA is an [[Linear Feedback Shift Register]] from [[Cipher Challenge 1]] encoded byte array. All BLOCKS from an ENTRY are combined and then decoded to reveal the stored information.

