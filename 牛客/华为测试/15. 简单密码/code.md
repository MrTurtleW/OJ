```python
import string

upper = string.ascii_uppercase
lower = string.ascii_lowercase

mapping = {}
for index, s in enumerate(['abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']):
    for ch in s:
        mapping[ch] = str(index + 2)


def convert(password):
    res = ""
    for ch in password:
        if ch in upper:
            ch = lower[(upper.index(ch) + 1) % len(upper)]
        elif ch in lower:
            ch = mapping[ch]

        res += ch

    return res

try:
    while True:
        password = input()
        print(convert(password))
except:
    # import traceback;traceback.print_exc()
    pass
```