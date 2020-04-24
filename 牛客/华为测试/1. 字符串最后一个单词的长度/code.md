```python
def get_last_length(s):
    length = len(s) - 1
    i = 0
    while length >= 0 and s[length] != ' ':
        i += 1
        length -= 1
    
    return i

s = input()
print(get_last_length(s))
```