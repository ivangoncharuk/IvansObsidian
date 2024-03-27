#ciphertech #job 

# Obfuscated JPEGs

During the same forensic investigation, multiple obfuscated JPEGs were discovered. All JPEGs start with the bytes FF D8 FF, but in this case, these bytes were changed to prevent applications from recognizing the files as JPEGs. All of these JPEGs are guaranteed to end with the standard magic bytes `FF D9`

The investigation requires that these JPEGs be identified and the initial bytes repairs so they can be viewed. Identifying the JPEGs should be a trivial task, but none of our tools are set up to recognize the custom header. Create a tool that, given an input file, can detect, extract, and save these obfuscated JPEGs. This process is commonly known as [[File Carving]] (with simple file repair).

Your program should...

- accept a path to a KDB file followed by another file path via command line arguments
- load the magic bytes from the KDB file's entry named "MAGIC" using the algorithm from [[Cipher Challenge 2]]. This file does not contain any obfuscated JPEGs.
- detect all JPEG files with the custom magic bytes that are present in the second provided file.
- replace the custom magic bytes from the KDB with the standard ones (`FF D8 FF`).
- output all repaired JPEGs to a directory "`<inputFileName>_Repaired`" in the same directory as the input file.
- save the repaired JPEGs with the filename "`<offset>.jpeg`".
- report to standard out the offset at which it detected each file, the file's size, the file's [[MD5]] hash (after it is repaired), and the path of the corresponding output file.
- should **NOT** attempt to OCR the repaired JPEGs to find the hidden message; just view them yourself.

Your solution to this challenge may not make use of any existing library for parsing JPEG files, [[File Carving]], file typing, or steganography. You may (and probably want to) use an existing [[MD5 implementation]].

