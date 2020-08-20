```java
class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0)
            return 0;

        int length = 0;
        int index = s.length() - 1;
        while (index >= 0 && s.charAt(index) == ' ')
            index --;
        for (; index >= 0; index--) {
            if (s.charAt(index) != ' ')
                length++;
            else
                break;
        }
        return length;
    }
}
```

