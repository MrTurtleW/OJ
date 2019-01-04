```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        start = result = 0
        for index in  range(len(s)):
            if s[index] in s[start:index]:
                start = start + s[start:index].index(s[index]) + 1
            elif result < index - start + 1:
                result = index - start + 1

        return result
```


```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        usedChar = {}
        
        for i in range(len(s)):
            if s[i] in usedChar and start <= usedChar[s[i]]:
                start = usedChar[s[i]] + 1
            else:
                maxLength = max(maxLength, i - start + 1)

            usedChar[s[i]] = i

        return maxLength
```