```python
try:
    while True:
        empty = int(input())
        if empty == 0:
            break
        drinks = 0
        while empty > 2:
            carry, val = divmod(empty, 3)
            drinks += carry
            empty -= carry * 2

        if empty == 2:
            drinks += 1

        print(drinks)

except:
    import traceback;traceback.print_exc()
```