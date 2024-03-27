#fall2023 #COSC-455

## Lecture Notes on Lexical Analysis for Mini-Language using Emacs Lisp

### General Structure of the Snippet

- The snippet is a `while` loop with a comparison operation (`x < 10`) and an assignment statement (`x := x - 1`).

### Tokenization
- Tokenization is the process of breaking down a source code snippet into "tokens" or individual pieces.

### Tokens in the snippet
`"while", "x", "<", "10", "do", "x", ":=", "x", "-", "1"`

### Types of Tokens

1. Keywords: `while`, `do`
2. Identifiers: `x`
3. Operators: `<`, `:=`, `-`
4. Literals: `10`, `1`

### Emacs Lisp Implementation Concepts

- Emacs Lisp can be used to build a lexer (lexical analyzer) that reads each character and classifies it into the respective token type.

### Sample Lisp Code for Tokenization

In Emacs Lisp, you could write a simple function that goes through a string and identifies tokens.

```lisp
(defun tokenize (input-string)
```

### Challenges

- Handling white-spaces and indentation.
- Dealing with syntactic sugar, if any.
- Resolving conflicts between keywords and identifiers (e.g., a variable named "while").

### Next Steps

After lexical analysis, the next stage is [[Syntactic Analysis (Parsing)]] where the token stream will be transformed into a parse tree or [[Abstract Syntax Tree]].
