

```python
def extended_euclid_algebraic(a, b):
    """
    Performs the Extended Euclidean Algorithm on integers a and b
    to find x, y such that ax + by = gcd(a, b), printing each step in algebraic format.
    """
    old_r, r = a, b
    old_s, s = 1, 0
    old_t, t = 0, 1
    
    print("Step by step process in algebraic format:")
    
    while r != 0:
        quotient = old_r // r
        # Print the current step in algebraic format before updating values
        print(f"{old_r}({old_s}) + {b}({old_t}) = {old_r}")
        
        old_r, r = r, old_r - quotient * r
        old_s, s = s, old_s - quotient * s
        old_t, t = t, old_t - quotient * t
    
    # Print the final step resulting in the gcd
    print(f"{old_r}({old_s}) + {b}({old_t}) = {old_r}")
    
    return old_s % b

# Find the modular inverse of 31 modulo 79 using the modified Extended Euclidean Algorithm
modular_inverse_algebraic = extended_euclid_algebraic(28, 89)
print(f"The modular inverse of 31 modulo 79 is {modular_inverse_algebraic}.")

```


 Find x and y so that 28x + 89y = 1.
 Find the inverse of 17 modulo 45.