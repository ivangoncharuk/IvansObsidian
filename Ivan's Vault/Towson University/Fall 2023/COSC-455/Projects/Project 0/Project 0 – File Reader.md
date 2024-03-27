#COSC-455 #fall2023 

### Requirements
- Use a programming language of your choice that supports recursion
- The path of the input files **should not** be hardcoded in, and should assume the file is in
the same relative path as the executable
- The program will read and display each character of an input file including character lines
and positions
- Every character including whitespaces should be 
	- displayed as is, 
	- on its own line in your output, 
	- with its position preceding it, 
	- and newlines can be converted to spaces
- All numbering for character positions should be displayed as **index 1 and not index 0**
- [[Project 0 gitignore]]
- [[COSC 455 Projects - Screenshots and Testing]]

- Exceptions must be handled in a user-friendly manner 
	- (File not found, IO, etc.) 
	- No overflow errors should occur 
- Filenames and paths must not be hardcoded 
- Empty input files must not crash the program 
- All code blocks and procedures must have descriptive code comments
- Effective version control (i.e. Git) commit messages are used 
- Code must compile successfully

---
### Overview

- The user is asked for a filename of an input text file 
- The program verifies the file exists and loads the file 
- The program reads the buffer containing the file character by character 
- As each character is read, the line and column of each character is displayed on the screen.
- The line, column, and character values are stored in global integer and string variables in the class of the program.
- When each character is being processed, the variables are overwritten with the current values

---
### ASCII Characters


		003 – ETX (End-of-Text for end of file)
		010 – LF (Line-Feed for new lines)
		013 – CR (Carriage-Return for new lines)

- Our provided input files will contain Unix-style LF line endings, not CRLF 
- Windows-style CRLF will not be an issue with the mini-language because it contains LF 
- Legacy Macintosh-style CR line endings will cause position reporting to fail

---
### Procedure nextChar()

- A global string **currentChar**() should be added with 
- Two global integer variables **currentLine**() and **currentColumn**() should be added
- A text input file will be loaded into memory in your project 
- Each time **nextChar**() is called, the variables should be populated with the details of a single character from the input file

---

- Initially, nextChar() will be called on its own after the input file has been loaded.
- A while loop with a condition of the currentChar() not being the End-of-Text character will run.
- The contents of the while loop will be calling nextChar() and printing the variable values. 
- The output should be printed to the screen in the format: 
	- 1:1 p 
		- where p is at the position line 1 column 1, 
	- 1:2 r 
		- and r is at position line 1 column 2 etc.

---

### Pseudocode for while-loop structure

```java 
// pre-test structure will not print ETX nextChar(); 
while ( currentChar() != ETX ) {
	print ( position() + “ “ + currentChar() ); 
	nextChar(); }```

```java
// post-test structure will always print ETX 
do { 
	nextChar(); print ( position() + “ “ + currentChar() ); 
} while ( currentChar() != ETX );
```

---

### Pseudocode for position()

```
// post-test structure will always print ETX 
Procedure position() { 
Return a string: currentLine() + “:” + currentColumn(); }
```

---
### Options I can choose

- There are many ways to implement **nextChar**() 
- **ReadByLines**() will read a given file buffer line by line returning a string for each line, and use a helper function to retrieve each character from the lines 
- **ReadByCharacters**() will read a given file buffer character by character, and handle LineFeed characters as new lines 
- Both functions would produce the same end-result output and be acceptable as an implementation of **nextChar**()

---

### Pseudocode for readByLines()
- A global string variable is used to store the currentLineValue() 
- Uses a companion function ReadByLinesHelper()

```
Procedure ReadByLines() { 
	// the end of a line is reached 
	if ( currentColumn() == (Size of currentLineValue() ) ) { 
		currentChar() := “ “; 
		currentLine() += 1; 
		currentColumn() := 0; 
	} 
	else if ( currentColumn() > 0 ) { 
		ReadByLinesHelper(); 
	} 
	else ( currentColumn() == 0 ) {
		if (next line == null ) {
			currentChar() := ETX; 
		} 
		else { 
			currentLineValue() := next line in file; 
			ReadByLinesHelper(); 
		} 
	}
```

---
### Pseudocode for readByLinesHelper()

- Helper companion procedure for the ReadByLines() 
- Similar to ReadByCharacters()

```
Procedure ReadByLinesHelper() { 
	retrieve the character at currentColumn() from currentLineValue(); 
	currentChar() := the retrieved character; currentColumn() += 1; 
}
```

---

### Pseudocode for ReadByCharacters()
```
Procedure ReadByCharacters() { 
	read the next character into memory ; 
	if LF character is found { 
		currentLine() += 1; 
		currentColumn() := 0; 
		currentChar() := “ “; 
	} 
	else { 
		retrieve next character as a string currentColumn() += 1; 
		currentChar() := the retrieved character;
	}
}
```

---


### Submission requirements

1. All sections of code must be commented in an organized manner. Individual procedures require a minimum of one explanatory comment above each block of code.

2. Libraries or modules for handling regular expressions are not permitted to be used. This includes, but is not limited to "re" in Python, and "regex" in Java and C++.

3. A plaintext README.md file (Word processor documents will not be accepted) must be included with your source code, containing the following information:
	a. Your first and last name.
	b. Programming Language used in your project, including the version number.
	c. The compiler or interpreter that is used to build or execute your project.
	d. The development environment, including any tools or IDEs used.
	e. Instructions to build or execute the program, such as using "make" or "javac".
	f. Complete documentation on end-user usage of the program, including all user input and output and command arguments.

4. If an IDE was used, please include related files and directories, such as ".idea" or ".vscode" directories for projects developed with IntelliJ, Clion, PyCharm, or Visual Studio Code.

5. Remove all binary executables of the project prior to submission. This includes but is not limited to ".class" ".pyc" ".o" ".exe" ".com".

6. In accordance with the Towson University Student Academic Integrity Policy, no plagiarism or academic dishonesty will be tolerated. Concepts and ideas may be discussed but sharing or reusing code is not accepted and will result in a minimum of a zero on the assignment. Consult the course syllabus for further details.

Requirements:
![[COSC 455 Project 0.pdf]]

