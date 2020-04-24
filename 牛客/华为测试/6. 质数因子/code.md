通过70%：

```python
from math import sqrt
from itertools import count, islice


def check_prime(n):
    """ https://stackoverflow.com/questions/4114167/checking-if-a-number-is-a-prime-number-in-python 
    
    trying to call range(n) for some n such that n > 2^31-1 (which is the maximum value for a C long) raises OverflowError. Therefore the best way to create a range generator is to use itertools
    """
    return n > 1 and all(n % i for i in islice(count(2), int(sqrt(n) - 1)))


def get_next_prime():
    number = 1
    while True:
        number += 1
        if check_prime(number):
            yield number


def split(n):
    res = []
    for prime in get_next_prime():
        if n < 2:
            break
        while n % prime == 0:
            res.append(prime)
            n = n // prime
    return res


try:
    while True:
        number = input()
        number = int(number)
        for item in split(number):
            print(item, end=" ")
except:
    pass
```