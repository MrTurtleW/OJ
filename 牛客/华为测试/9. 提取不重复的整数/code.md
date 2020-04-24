```python
try:
    while True:
        s = input()
        res = ''
        _set = set()
        for char in s[::-1]:
            if char not in _set:
                res += char
                _set.add(char)

        print(res)
except:
    pass
```