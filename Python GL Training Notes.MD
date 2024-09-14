## Floating Point Numbers
```python
print(1.2 - 1.0) # is 0.19999999

print(round(1.2 - 1.0, 2)) # is 0.2
```

**Python Decimal Packages:**
```python
from decimal import Decimal, getcontext

# getcontext().prec = 3

Decimal(3.14) # is 3.140000000000000124344978758017532527446746826171875
Decimal('3.14') # is 3.14
```

## Boolean

Values like 0, "", None, [], {}, (), 0.0 are all false.
```python
num = []
if num:
    print(f"{num} is not False")
else:
    print(f"{num} is False")

# Outputs: [] is False
```

**Logic Building:**
```python
bikeIsOk = True
weatherIsNice = True
```
If both the values are true then outcome is true. So if we create a truth table.

| bikeIsOk | weatherIsNice | Go for Ride |
| -------- | ------------- | ----------- |
| 0        | 0             | 0           |
| 1        | 0             | 0           |
| 0        | 1             | 0           |
| 1        | 1             | 1           |
So, this is clearly an `and` logic.

```python
bikeIsOk = True
weatherIsNice = True

if bikeIsOk and weatherIsNice:
    print("Go for a ride")
else:
    print("Stay at home")
```

Another example:
```python
isWeekend = True
haveFreeTime = True
```
If either of the values are true then result is true. So the truth table is 

| isWeekend | haveFreeTime | Go for Ride |
| --------- | ------------ | ----------- |
| 0         | 0            | 0           |
| 1         | 0            | 1           |
| 0         | 1            | 1           |
| 1         | 1            | 1           |
So, this is clearly an `or` logic.

```python
isWeekend = True
haveFreeTime = False

if isWeekend or haveFreeTime:
    print("Go for a ride")
else:
    print("Stay at home")
```

# Lists

Lists are subscriptable. 
If the length of the object is already known prefer using tuple.

**Insert element:**
```python
# Insert element in list
my_list = [1,2,3,4,5]

# at the end of the list
my_list.append(6)
print(my_list) # Outputs: [1, 2, 3, 4, 5, 6]

# At a specific position
my_list.insert(0, 0)
print(my_list) # Outputs: [0, 1, 2, 3, 4, 5, 6]
```

**Remove element:**
```python
# Insert element in list
my_list = [0, 1, 2, 3, 4, 5, 6]

# from the end of the list
my_list.pop()
print(my_list) # Outputs: [0, 1, 2, 3, 4, 5]

# A specific value
my_list.remove(0)
print(my_list) # Outputs: [1, 2, 3, 4, 5]
```

**Copy list:**
```python
my_list = [0, 1, 2, 3, 4, 5, 6]
# Copy of the list
another_list = my_list.copy() # Soft copy

my_list.pop() # Remove last element
print(another_list) # Outputs: [0, 1, 2, 3, 4, 5, 6]
```

**Clear a list:**
```python
my_list = [0, 1, 2, 3, 4, 5, 6]

# using clear method
my_list.clear()

# using *=0
my_list*=0

# using del keyword
del my_list[:]
```

# Set

Sets are not subscriptable. Sets are independent of order of elements. Set does not contain duplicate values.

**Add element in set**

```python
my_set = {1,2}
my_set.add(3)
print(my_set) # Outputs: {1, 2, 3}
```

**Remove element from list:**
```python
my_set = {1,2}

# Using pop method tp remove random item from list
my_set.pop()
print(my_set) # Outputs: {2}

# Using discard method to remove specific item from list
my_set = {1,2}
my_set.discard(2)
print(my_set) # Outputs: {1}
```

# Exceptions

**Order of the exception:**
The most general error should be at last.

```python
try:
    1/0
except ZeroDivisionError:
    print("ZeroDivisionError error catch")
except Exception:
    print("Exception error catch")

# Outputs: ZeroDivisionError error catch

try:
    1/0
except Exception:
    print("Exception error catch")
except ZeroDivisionError:
    print("ZeroDivisionError error catch")

# Outputs: Exception error catch
```

**Create Specific Exceptions:**

```python
class PaymentFailedException(Exception):
    ...

class NotSufficientAmount(PaymentFailedException):
    def __init__(self, amount):
        super().__init__(f"Your current amout is {amount} which is too low")

class InvalidCard(PaymentFailedException):
    def __init__(self, last_four):
        super().__init__(f"Your card ****{last_four} is not a valid card")

def makePayment(card):
    cards = {
        "1122334455667788": 30,
        "8877665544332211": 0
    }

    balance = cards.get(card)
    if balance != 0 and not balance:
        raise InvalidCard(card[-4:])

    if balance <= 0:
        raise NotSufficientAmount(balance)

    print(f"Payment successfully deducted from {card}")
```

**Use of descriptor:**

```python
class MailDescriptor:
    def __init__(self):
        print("Constructor")

    def __get__(self, obj, objType=None):
        return obj.__data

    def __set__(self, obj, value):
        print("Setter method")
        self.validate(value)
        obj.__data = value

    def validate(self, value):
        if not isinstance(value, str):
            raise Exception("Not a strinng")

class Person:
    email = MailDescriptor()

    def __init__(self, *, email):
        self.email = email


Person(email=123)
```
