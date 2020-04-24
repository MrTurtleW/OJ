```python
def check_password(password):
    if len(password) <= 8:
        return False

    sub_str = set()
    # upper lower number other
    _list = [False] * 4
    for index, ch in enumerate(password):
        if 'A' <= ch <= 'Z':
            _list[0] = True
        elif 'a' <= ch <= 'z':
            _list[1] = True
        elif '0' <= ch <= '9':
            _list[2] = True
        else:
            _list[3] = True

        if index < len(password) - 2 and password[index:index+3] in sub_str:
            return False
        else:
            sub_str.add(password[index:index+3])

    if _list.count(True) < 3:
        return False
    return True


try:
    while True:
        password = input()
        if check_password(password):
            print('OK')
        else:
            print('NG')
except:
    # import traceback;traceback.print_exc()
    pass
```