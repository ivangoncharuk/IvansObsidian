```python
def extended_euclid(a, b):
    """
    Extended Euclidean Algorithm to find integers x and y such that ax + by = gcd(a, b)
    and print the steps sequentially.
    
    Parameters:
    - a: First number
    - b: Second number
    
    Returns:
    The integers x and y.
    """
    x0, x1, y0, y1 = 1, 0, 0, 1
    while b != 0:
        q, a, b = a // b, b, a % b
        x0, x1 = x1, x0 - q * x1
        y0, y1 = y1, y0 - q * y1
        print(f"Step: a = {a}, b = {b}, q = {q}, x = {x0}, y = {y0}")
    return x0, y0

# Find x and y for 11x + 52y = 1
x, y = extended_euclid(11, 52)
print(f"\nSolution: x = {x}, y = {y}")

```

