```python
import sys


def check_ip(ip):
    nums = ip.split('.')
    if len(nums) != 4:
        return False

    for n in nums:
        try:
            assert n != ''
            assert 0 <= int(n) <= 255
        except AssertionError or ValueError:
            return False

    return True


def check_mask(mask):
    if mask in ['255.255.255.255', '0.0.0.0']:
        return False

    if not check_ip(mask):
        return False

    mask_array = [0] * 32
    for index, item in enumerate(mask.split('.')):
        item = int(item)
        for i in range(8):
            if item == 0:
                break
            item, left = divmod(item, 2)
            if left:
                mask_array[index * 8 + 7 - i] = 1

    if 32 - mask_array[::-1].index(1) > mask_array.index(0):
        return False

    return True


def is_private(ip):
    if ip.startswith('10.'):
        return True
    elif ip.startswith('192.168.'):
        return True
    elif ip.startswith('172.') and 16 <= int(ip.split('.')[1]) <= 31:
        return True
    else:
        return False


def label_cls(ip):
    first = int(ip.split('.')[0])
    if 1 <= first <= 126:
        return 'a'
    elif 128 <= first <= 191:
        return 'b'
    elif 192 <= first <= 223:
        return 'c'
    elif 224 <= first <= 239:
        return 'd'
    elif 240 <= first <= 255:
        return 'e'
    else:
        return 'ignore'

try:
    res = {
        'a': 0,
        'b': 0,
        'c': 0,
        'd': 0,
        'e': 0,
        'invalid': 0,
        'private': 0,
        'ignore': 0,
    }
    while True:

        ip, mask = input().split("~")
        if ip.startswith('0.'):
            continue

        if not check_mask(mask):
            res['invalid'] += 1

        elif not check_ip(ip):
            res['invalid'] += 1
        else:
            if is_private(ip):
                res['private'] += 1
            res[label_cls(ip)] += 1

except:
    # import traceback;traceback.print_exc()
    print(' '.join(map(str, map(res.get, ['a', 'b', 'c', 'd', 'e', 'invalid', 'private']))))
```