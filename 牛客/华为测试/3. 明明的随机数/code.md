```python
try:
    while True:
        a = []
        count = input()
        count = int(count)
        for i in range(count):
            temp = input()
            a.append(int(temp))

        a = sorted(set(a))
        for item in a:
            print(item)
except:
    pass
```