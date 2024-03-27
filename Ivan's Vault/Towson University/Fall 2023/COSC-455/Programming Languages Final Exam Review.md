---
tags:
  - COSC-455
  - fall2023
---
Subprograms, also known as functions or procedures, are a fundamental concept in programming. Understanding their components and how they work is crucial for effective programming. Here's an intuitive explanation of the key concepts:

## Formal Parameters vs. Actual Parameters

- **Formal Parameters**: These are the variables defined in the subprogram's signature. They act as placeholders for values that will be passed to the subprogram when it's called.
  
  For example, in `def add(x, y)`, `x` and `y` are formal parameters.

- **Actual Parameters**: These are the real values or expressions passed to the subprogram when it's called.

  For example, in `add(5, 3)`, `5` and `3` are actual parameters.

## Parameter Passing Methods

Different languages and environments use various methods for passing parameters to subprograms:

1. **Call by Value**: The actual parameter's value is copied into the formal parameter. Inside the subprogram, the formal parameter acts as a local variable.

2. **Call by Value-Result**
- Similar to call by value, but when the subprogram finishes, the formal parameter's value is copied back to the actual parameter.
- Similar to call by value, but upon completion of the method, the modified value of the parameter is copied back into the original variable. This can lead to changes in the original variable after the method execution, unlike call by value.

4. **Call by Reference**: 
- The actual parameter's reference (memory address) is passed. The formal parameter becomes an alias for the actual parameter, allowing direct modification of the actual parameter.
- The actual parameter's memory address is passed to the method, allowing the method to modify the actual parameter directly.

5. **Call by Name**: Parameters are passed as expressions that are evaluated every time they're used inside the subprogram. This can lead to different results than expected if the expressions change between calls.

### Examples

```c
int multiplyByTwo(int a) {
  a = a * 2;
  return a;
}

int main() {
  int x = 5;
  int result = multiplyByTwo(x);
  printf("x = %d, result = %d\n", x, result);
  return 0;
}
```

1. **Call by Value:**
	- What will be the value of **x** after the function call?
		- 5
	- What will be the value of **result** after the function call?
		- 10
	- Explain your reasoning.
		- Since it is pass-by-value, just the value of `x` is passed into `multiplyByTwo`
		- This means that the value of `x` is not being changed, but the result is being set by the return value of `multiplyByTwo`

1. **Call by Value-Result:**
    
    - What will be the value of **x** after the function call?
    - What will be the value of **result** after the function call?
    - Explain your reasoning.
    
5. **Call by Reference:**
    
    - What will be the value of **x** after the function call?
    - What will be the value of **result** after the function call?
    - Explain your reasoning.
    
7. **Call by Name:**
    
    - What will be the value of **x** after the function call?
    - What will be the value of **result** after the function call?
    - Explain your reasoning.


## Variables and Their Attributes

Variables in programming have several key attributes:

1. **Name**: The identifier used in the code.
2. **Address**: The memory location where the variable is stored.
3. **Type**: The data type of the variable (e.g., integer, string).
4. **Value**: The current value stored in the variable.
5. **Lifetime**: The duration for which the variable exists in the program.
6. **Scope**: The area of the program where the variable can be accessed.

## Binding and Binding Time

Binding refers to the association of various attributes (like type or value) with variables:

- **Static Binding**: Done at compile-time and doesn't change at runtime.
  - *Static Type Binding*: The variable's type is fixed at compile-time.
  
- **Dynamic Binding**: Done at runtime.
  - *Dynamic Type Binding*: The variable's type can be set and changed during execution.
  - *Example*: In Python, `x = 5` binds `x` as an integer, but later `x = "hello"` changes its type to string.

## Scope: Static vs. Dynamic

- **Static Scope**: The region where a variable is accessible is determined at compile time. Most modern languages use static scope.

- **Dynamic Scope**: The region where a variable is accessible is determined at runtime based on the calling sequence of subprograms.

## Implementing Dynamic Scope

- **Deep Access**: Searches for variable bindings starting from the most recent call to the least recent. Involves following dynamic links and searching inside frames.

- **Shallow Access**: Uses a central store (like a hash table) for all variable bindings. Faster but can be complex to manage.

## Implementing Static Scope

- **With Nested Programs**: Use static links to reference the environment of outer scopes. Represent each variable with a pair (chain_offset, local_offset).
- **Without Nested Subprograms (e.g., C Language)**: Static links are unnecessary as there's no nested scope to manage.

---


### Assignment 8

```
void sub3() {
    int x, z;
    x = u + v;
    . . .
}
void sub2() {
    int w, x;
    . . .
}
void sub1() {
    int v, w;
    . . .
}
void main() {
    int v, u;
    . . .
}
```

1. Show the run-time stack during the execution of function sub3 after the following calling sequence (all the details must be included).
    
    - main calls sub1
    - sub1 calls sub1
    - sub1 calls sub2
    - sub2 calls sub3
2. Consider the reference to variable u in function sub3.
    
    - (a) Write the sequence of activation record instances that must be searched in order to find u.
        - sub3, sub2, sub1, sub1, main
    - (b) How many dynamic links must be followed?
        - 4
3. Consider the reference to variable v in function sub3.
    
    - (a) Write the sequence of activation record instances that must be searched in order to find v.
        - sub3, sub2, sub1
    - (b) How many dynamic links must be followed?
        - 2

#### Question 2

Consider the following program in a static-scoped language.

```
program P;
bool a,b;
procedure A;
bool a;
procedure C;
begin
    if a then C;
end C;
begin
    a := true;
    if a != b then B <-------- point 1
end A;
procedure B;
begin
    if a then A <-------- point 2
end B;
begin
    a := b := false;
    A
end P.

```

1. For each subprogram list the name of subprograms that are visible inside it.
    
    - subprogram visible subprograms
        - P: A, B
        - A: P, A, B, C
        - B: P, A, B
        - C: P, A, B, C
2. Calculate the static depth of the following subprograms:
    
    - P: 0
    - A: 1
    - B: 1
    - C: 2
3. Calculate chain offset of the following variables:
    
    - (a) variable a at point 1
        - 0
    - (b) variable b at point 1
        - 1
    - (c) variable a at point 2
        - 1
4. Show the run-time stack during the execution of B (all the details must be included).

![[Pasted image 20231212145043.png | 800]]

### Assignment 6

1. **Write the function dot-product of two vectors l1 and l2** that multiplies corresponding numbers in l1 and l2 and builds a new number by summing the results. The vectors are the same length.
    
    Example: `(dot-product ’(1 2 3) ’(3 2 4))` returns 19.
```lisp
(defun member (a l)
  (cond
    ((null l) ())
    ((eq a (car l)) t)
    (t (member a (cdr l)))
  )
)
(defun subset (l1 l2)
  (cond
    ((null l1) t)
    ((member (car l1) l2) (subset (cdr l1) l2))
    (t ())
  )
)
```
    
2. **Write the function subset** which takes two lists l1 and l2 and returns true if l1 is a subset of l2.
    
    Examples:
    
    - `(subset ’(1 2) ’(0 3 2 1))` is true.
    - `(subset ’(1 2) ’(0 3 2 4))` is false.
    - `(subset () ’(0 3 2 1))` is true.
```lisp
(defun member (a l)
  (cond
    ((null l) ())
    ((eq a (car l)) t)
    (t (member a (cdr l)))
  )
)
(defun subset (l1 l2)
  (cond
    ((null l1) t)
    ((member (car l1) l2) (subset (cdr l1) l2))
    (t ())
  )
)
```

**Write the function insertL** which takes three arguments: the atoms new and old, and a list of atoms. It builds a list with new inserted to the left of the first occurrence of old.

Example: `(insertL ’fudge ’fruit ’(ice cream with fruit for dessert))` returns (ice cream with fudge fruit for dessert).
```lisp
(defun insertL (new old l)
  (cond
    ((null l) ())
    ((eq old (car l)) (cons new l))
    (t (cons (car l) (insertL new old (cdr l))))
  )
)
```

**Write the function substall** which takes three arguments: the atoms new and old, and a list of atoms. It builds a list in which all occurrences of old are replaced by new.

`(substall ’fudge ’fruit ’(ice cream with fruit and more fruit))` returns (ice cream with fudge and more fudge).

```
(defun substall (new old l)
  (cond
    ((null l) ())
    ((eq old (car l)) (cons new (substall new old (cdr l))))
    (t (cons (car l) (substall new old (cdr l))))
  )
)
```

**Write the function rember2** which takes two arguments: an atom a and a list of atoms l and removes the second occurrence of a in l.

Examples:

- `(rember2 ’fudge ’(ice cream with fruit for dessert))` returns (ice cream with fruit for dessert).
- `(rember2 ’ice ’(ice cream with fruit and ice cream with fudge))` returns (ice cream with fruit and cream with fudge).
- `(rember2 ’ice ())` returns ().

Hint: Use the function rember that we wrote in class.

```lisp
(defun rember (x l)
  (cond
    ((null l) l)
    ((eq x (car l)) (cdr l))
    (t (cons (car l) (rember x (cdr l))))
  )
)
(defun rember2 (x l)
  (cond
    ((null l) l)
    ((eq (car l) x) (cons (car l) (rember x (cdr l))))
    (t (cons (car l) (rember2 x (cdr l))))
  )
)

```


**Write the function occurN** which takes two lists l1 and l2 and counts how many times an atom in l1 occurs in l2.
Examples:

- `(occurN ’(fudge ice cream) ’(ice cream with fruit for dessert))` returns 2.
- `(occurN ’(fudge fruit) ’(ice cream with fruit for dessert))` returns 1.
- `(occurN ’(fudge ice cream) ())` returns 0.
```lisp
(defun count (x l)
  (cond
    ((null l) 0)
    ((eq x (car l)) (+ 1 (count x (cdr l))))
    (t (count x (cdr l)))
  )
)
(defun occurN (l1 l2)
  (cond
    ((null l1) 0)
    (t (+ (count (car l1) l2) (occurN (cdr l1) l2)))
  )
)
```

**Write the function pair** which takes two lists l1 and l2 of the same length and returns a list of two-element lists containing successive pairs of an element from each.

Example: `(pair ’(a b c ) ’(1 2 3))` returns ((a 1) (b 2) (c 3)).

```lisp
(defun pair (l1 l2)
  (cond
    ((and (null l1) (null l2)) ())
    (t (cons (list (car l1) (car l2)) (pair (cdr l1) (cdr l2))))
  )
)
```

**Write a function assoc** that takes an atom x and a list l of the form created by pair (in the previous question) and returns the second element of the first list in l whose first element is x.

Example: `(assoc y ’((x a) (y b) (z c)))` returns b.

```
(defun assoc (x l)
  (cond
    ((null l) ())
    ((eq x (caar l)) (car (cdr (car l))))
    (t (assoc x (cdr l)))
  )
)
```

