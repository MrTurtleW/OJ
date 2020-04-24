```python
try:
    while True:
        s = input()
        left = len(s) % 8
        if left != 0:
            s = s + '0' * (8-left)
        for i in range(0, len(s), 8):
            print(s[i:i+8])
except:
    pass
```