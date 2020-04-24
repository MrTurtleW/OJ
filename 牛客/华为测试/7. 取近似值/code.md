```python
try:
    while True:
        a = float(input())
        a_int = int(a)
        if a - a_int >= 0.5:
            print(a_int + 1)
        else:
            print(a_int)
except:
    pass
```