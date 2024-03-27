---
tags:
  - fall2023
  - COSC-455
---

# Keybindings
## Basic Keybindings

In Emacs, actions are performed through commands, which can be invoked through keybindings or by name using `M-x` (Meta key followed by `x`). Here's a list of some basic keybindings and their descriptions:

- **Moving the Cursor**:
    - `C-f`: Move forward one character (f for forward).
    - `C-b`: Move backward one character (b for backward).
    - `C-n`: Move to the next line (n for next).
    - `C-p`: Move to the previous line (p for previous).

- **Editing**:
    - `C-d`: Delete the character under the cursor (d for delete).
    - `C-k`: Kill (cut) from the cursor to the end of the line (k for kill).
    - `C-y`: Yank (paste) the killed text (y for yank).
    - `C-/`: Undo the last change.

- **Saving and Exiting**:
    - `C-x C-s`: Save the current buffer (s for save).
    - `C-x C-c`: Exit Emacs (c for close).

## Lisp-Specific Keybindings

When working with Emacs Lisp, you'll often deal with expressions, which are pieces of code that can be evaluated to produce a value. Here are some keybindings and commands specific to working with Lisp:

- **Evaluating Expressions**:
    - `C-x C-e`: Evaluate the Lisp expression before the cursor and display the result.
    - `M-x eval-region`: Evaluate all expressions in the selected region.
    - `M-x eval-buffer`: Evaluate all expressions in the current buffer.

- **Documentation**:
    - `C-h f`: Look up documentation for a function (f for function).
    - `C-h v`: Look up documentation for a variable (v for variable).

- **Interactive Lisp Session**:
    - `M-x ielm`: Start an interactive Emacs Lisp session.

## Understanding S-expressions (sexps)

In Lisp, code and data are written as S-expressions, or sexps. An S-expression is a parenthesized expression, like `(function arg1 arg2)`. Sexps can be nested, which is fundamental to Lisp's structure. Keybindings like `C-M-f` (move forward over a sexp) and `C-M-b` (move backward over a sexp) help navigate through code by jumping from one balanced expression to another.

## Formatting and Indentation

Proper formatting is crucial for readability. In Lisp, indentation helps signify the structure of the code:

- `M-x indent-region`: This command indents all the lines in the selected region based on the Lisp syntax, helping to visually represent the nesting of expressions.

This breakdown covers fundamental keybindings and concepts essential for working with Emacs Lisp in a more intuitive manner, making it easier to understand why certain keybindings are structured the way they are and how they relate to the language's syntax and structure.

# Lisp Basic Knowledge
# Values and Types

Emacs Lisp has a variety of data types to represent different kinds of information.

### Numbers

Numbers can be integers or floating-point. Examples:

```lisp
123   ;; an integer
-456  ;; a negative integer
3.14  ;; a floating-point number
```

### Strings

Strings are sequences of characters enclosed in double quotes:

```lisp
"This is a string"
```

### Symbols

Symbols are unique and immutable data objects. They are often used as identifiers:

```lisp
'symbol     ;; This is a symbol
```

### Cons Cells

A cons cell is a pair of values. Cons cells can be used to build lists:

```lisp
(cons 1 2)    ;; This is a cons cell, its car is 1 and its cdr is 2
```

### Lists

Lists are chains of cons cells, or the empty list `nil`. Here's a simple list:

```lisp
'(1 2 3)   ;; This is a list of three elements
```

### Arrays

Arrays are ordered collections of elements, accessible by an index. Strings and vectors are types of arrays.

### Vectors

Vectors are like lists, but they allow faster access to individual elements:

```lisp
[1 2 3]   ;; This is a vector of three elements
```

### Examples of Values

```lisp
123             ;; a number
"This is text"  ;; a string
'my-symbol      ;; a symbol
(cons 1 2)      ;; a cons cell
'(1 2 3)        ;; a list
[1 2 3]         ;; a vector
```

- Emacs has a built-in tutorial and extensive documentation which can be accessed with the `C-h` (Control + h) key sequence followed by the appropriate key 
- (e.g., `C-h t` for the tutorial, `C-h i` for info documentation).


# Examples
### pick function
The `pick` function as written by your instructor:

```lisp
(defun pick (n l)
  (cond
    ((null l) l)              ; If the list is empty, return it.
    ((eq n 1) (car l))        ; If n is 1, return the first item of the list.
    (t (pick (- n 1) (cdr l))) 
    ; else, recursively call `pick` with n decremented by 1 and the rest of the list.
  )
)
```

- `defun`: Defines a new function named `pick`.

- `(n l)`: The parameters for the function, where `n` is the 1-based index of the item to return, and `l` is the list.

- `cond`: The `cond` expression is a conditional construct that evaluates each clause until one returns true. Each clause has a condition and an expression to evaluate if the condition is true.

- `((null l) l)`: The first clause checks if the list is empty using the `null` function. If it is, it returns the list itself, which is empty.

- `((eq n 1) (car l))`: The second clause checks if `n` is 1 using the `eq` function for equality comparison. If so, it returns the first item of the list, obtained with `car`.

- `(t (pick (- n 1) (cdr l)))`: The final clause is the default case, indicated by `t` for true. If none of the previous conditions were true, it recursively calls `pick` with `n` decremented by 1 (using `- n 1`), and the rest of the list (using `cdr l`).

The function operates recursively, removing the first element of the list and decrementing `n` until `n` is 1, at which point it returns the first element of the current list, which corresponds to the n'th element of the original list. This is a common recursive pattern in Lisp for traversing and processing lists.





[[Lisp Notes]]
[[More Lisp Exercises]]