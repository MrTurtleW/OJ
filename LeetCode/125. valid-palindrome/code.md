# 自己写的

```python
import string
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = ''.join([char.lower() for char in s if char in string.ascii_letters + string.digits])
        i, j = 0, len(s)-1

        while i < j:
            if s[i] == s[j]:
                i += 1
                j -= 1
            else:
                return False

        return True
```

直接写`abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789`速度会快一点（64ms到44ms）

下面这种会慢一点（52ms），内存没区别

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = ''.join([char.lower() for char in s if char in 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'])
        i = 0

        while i < len(s) - i - 1:
            if s[i] == s[len(s)-i-1]:
                i += 1
            else:
                return False

        return True
```

48ms-13.3MB

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        i, j = 0, len(s) - 1

        while i < j:
            si = s[i].lower()
            sj = s[j].lower()

            if not si in 'abcdefghijklmnopqrstuvwxyz0123456789':
                i += 1
            elif not sj in 'abcdefghijklmnopqrstuvwxyz0123456789':
                j -= 1
            elif si != sj:
                return False

            else:
                i += 1
                j -= 1

        return True
```

java-6ms-39MB

```java
class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if ("abcdefghijklmnopqrstuvwxyz0123456789".indexOf(s.charAt(i)) != -1){
                sb.append(s.charAt(i));
            }
        }

        String origin = sb.toString();
        String reversed = sb.reverse().toString();

        if(reversed.equals(origin))
            return true;
        return false;
    }
}
```