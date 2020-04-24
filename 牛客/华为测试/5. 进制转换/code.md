```python
mapping = {hex(i)[2:].upper(): i for i in range(16)}
try:
    while True:
        hex_str = input()
        result = 0
        for i, ch in enumerate(hex_str[:1:-1]):
            result += mapping[ch] * pow(16, i)
        print(result)
except:
    pass
```