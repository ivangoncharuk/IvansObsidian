---
tags:
  - spring2024
  - COSC-436
---

Encapsulation is a fundamental concept in [[Object Oriented Programming]] (OOP) that involves bundling the data (**attributes**) and **methods** (functions) that operate on the data into a single unit, known as a **class**. 

It also restricts direct access to some of the object's components, which is a way of preventing accidental modification of data. 

This is achieved through the use of access modifiers, making some class members private and others public.

## Code Example (Python)

```python
class Account:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance  # Private attribute

    def deposit(self, amount):
        self.__balance += amount
        print("Deposit Successful")

    def withdraw(self, amount):
        if amount > self.__balance:
            print("Insufficient funds")
        else:
            self.__balance -= amount
            print("Withdrawal Successful")

    def get_balance(self):
        return self.__balance

# Creating an instance
acc = Account("John Doe", 1000)
acc.deposit(500)
print(acc.get_balance())
acc.withdraw(200)
