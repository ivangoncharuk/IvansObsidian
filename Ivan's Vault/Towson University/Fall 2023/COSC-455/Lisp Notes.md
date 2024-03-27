
## Functions
### Function: `len` (Length of a List)
```lisp
(defun len (lst)
  "Calculate the length of a list."
  (if (null lst)
      0
    (+ 1 (len (cdr lst)))))
```

### Function: `reverse-list` (Reverse a List)
```lisp
(defun reverse-list-helper (lst acc)
  "Helper function for reverse-list."
  (if (null lst)
      acc
    (reverse-list-helper (cdr lst) (cons (car lst) acc))))

(defun reverse-list (lst)
  "Reverse a list."
  (reverse-list-helper lst nil))
```

### Function: `dot-product` (Dot Product of Two Vectors)
```lisp
(defun dot-product (l1 l2)
  "Calculate the dot product of two lists."
  (if (or (null l1) (null l2))
      0
    (+ (* (car l1) (car l2))
       (dot-product (cdr l1) (cdr l2)))))
```

### Function: `rember` (Remove First Occurrence)
```lisp
(defun rember (a lat)
  "Remove the first occurrence of 'a' from the list."
  (cond
    ((null lat) nil)
    ((equal (car lat) a) (cdr lat))
    (t (cons (car lat) (rember a (cdr lat))))))
```

### Function: `insertL` (Insert Left of an Element)
```lisp
(defun insertL (new old l)
  "Insert 'new' to the left of the first occurrence of 'old'."
  (cond
    ((null l) ())
    ((eq old (car l)) (cons new l))
    (t (cons (car l) (insertL new old (cdr l))))))
```

### Function: `substall` (Substitute All Occurrences)
```lisp
(defun substall (new old lat)
  "Substitute all occurrences of 'old' with 'new'."
  (cond
    ((null lat) nil)
    ((equal (car lat) old) (cons new (substall new old (cdr lat))))
    (t (cons (car lat) (substall new old (cdr lat))))))
```


---

## Writing Recursive Functions in Lisp

### Step-by-Step Guide

1. **Identify the Base Case:** Determine the simplest, smallest input for which you can provide an immediate answer.
2. **Solve the Base Case:** Implement the solution for the base case.
3. **Recursive Step:** Break down the problem into smaller instances of the same problem.
4. **Call the Function Recursively:** Implement the recursive call with a smaller or simpler input.
5. **Unwinding the Recursion:** Ensure that each recursive call contributes to the final answer.

### Tools for Recursion in Lisp

- **`if` or `cond`:** For decision-making between base and recursive cases.
- **`car`:** To access the first element of a list.
- **`cdr`:** To access the remainder of a list (all but the first element).
- **`cons`:** To construct lists or add elements to the front of a list.
- **Helper Functions:** Auxiliary functions to handle complex tasks.

---

## Understanding Cons Cells, Lists, and Atoms in Lisp

### Cons Cells
- A cons cell is a fundamental building block in Lisp, representing a pair of values.
- Notation: `(cons a b)` creates a cons cell with `a` as the car (first part) and `b` as the cdr (second part).

### Lists
- A list in Lisp is a chain of cons cells, where each cell's cdr points to the next cell.
- Notation: `'` (quote) is used to create a list literally, e.g., `'(a b c)` is a list of three elements.
- Empty List: `nil` or `'()` represents an empty list.

### Atoms
- An atom is a basic unit that is not a cons cell. It includes numbers, symbols, and other primitive types.
- In context: In a list, each element can be an atom or another list.