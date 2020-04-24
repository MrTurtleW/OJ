```python
def count_char(s, c):
    count = 0
    s = s.lower()
    c = c.lower()
    for char in s:
        if c == char:
            count += 1
    return count

s = input()
c = input()
print(count_char(s, c))
```