```python
try:
    while True:
        res = {}
        n = int(input())
        for i in range(n):
            key, value = input().split()
            key = int(key)
            if key in res:
                res[key] += int(value)
            else:
                res[key] = int(value)

        for k in sorted(res.keys()):
            print(k, res[k])
except:
    pass
```