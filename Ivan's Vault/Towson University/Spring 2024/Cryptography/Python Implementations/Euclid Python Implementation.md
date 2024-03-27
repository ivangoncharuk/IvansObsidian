```python
def gcd(a, b):
    """
    Compute the greatest common divisor (GCD) of two numbers using Euclid's Algorithm.
    
    Parameters:
    - a: First number
    - b: Second number
    
    Returns:
    The GCD of a and b.
    """
    while b != 0:
        a, b = b, a % b
    return a

# Example usage with gcd(119, 91)
gcd_result = gcd(119, 91)
print(gcd_result)
```


