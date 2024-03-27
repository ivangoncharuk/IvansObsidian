

### Function `sum-odd-numbers`
```lisp
(defun is-odd (n) (eq (mod n 2) 1) )

(defun sum-odd-numbers (lst)
  "If lst is empty, return 0"
  (cond
   ( (null lst)
     0 )
   "If (car lst) is odd, add it to the sum obtained from the recursive call with (cdr lst)"
   ( (is-odd (car lst))
     (+ (car lst) (sum-odd-numbers (cdr lst)))
     )
   "Otherwise, just make the recursive call with (cdr lst)"
   (t (sum-odd-numbers (cdr lst)))
   )
  )
(sum-odd-numbers mylist) ; 25
```

### Function `remove duplicates`

```lisp
 ;; (5 9 9 7 7 8) -> (5 9 7 8)

(setq mylist '(5 6 6 6 7 7 9 0 0 7))

(defun member (n lst)
  (cond
   ((null lst) ())
   ((= n (car lst)) t)
   (t (member n (cdr lst)))
   )
  )

 (defun remove-duplicates (lst)
   (cond
  ;; If the list is empty, return an empty list
   ((null lst) ())
   ;; Check if the first element is in the rest of the list
   ( (member (car lst) (cdr lst))
     ;; If it is, omit it and recur with the rest of the list
     (remove-duplicates (cdr lst)))
   ;; If not, include it and recur with the rest of the list
   (t (cons (car lst) (remove-duplicates (cdr lst))) )
   )
   )

(remove-duplicates mylist) ; (5 6 9 0 7)
```

