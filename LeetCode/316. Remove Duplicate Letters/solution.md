# 贪心

```java
class Solution {

    public String removeDuplicateLetters(String s) {
        if (s.length() == 0)
            return "";
        int[] count = new int[26];

        for (int i =0; i<s.length(); i++) {
            count[s.charAt(i)-'a'] ++;
        }

        int pos = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) < s.charAt(pos))
                pos = i;

            if (--count[s.charAt(i)-'a'] == 0)
                break;
        }

        return s.charAt(pos) + removeDuplicateLetters(s.substring(pos+1).replaceAll(s.charAt(pos) + "", ""));
    }
}
```

给定一个字符串，贪心的选择（答案中最左边的字符）是满足以下条件的最小的`s[i]`：`s[i:]`含有全部不同字符。

# 栈

```java
import java.util.Stack;

class Solution {

    public String removeDuplicateLetters(String s) {
        if (s.length() == 0)
            return "";
        int[] count = new int[26];

        for (int i =0; i<s.length(); i++) {
            count[s.charAt(i)-'a'] ++;
        }

        Stack<Character> st = new Stack<>();

        for (char ch: s.toCharArray()) {
            count[ch - 'a']--;
            if (st.contains(ch))
                continue;

            while (!st.isEmpty() && ch < st.peek() && count[st.peek()-'a'] > 0)
                st.pop();

            st.push(ch);
        }
        
        StringBuilder builder = new StringBuilder();
        
        while (!st.isEmpty()) {
            builder.insert(0, st.pop());
        }
        
        return builder.toString();
    }
}
```

# 迭代

The basic idea is to find out the smallest result letter by letter (one letter at a time). Here is the thinking process for input "cbacdcbc":

1. find out the last appeared position for each letter;
   c - 7
   b - 6
   a - 2
   d - 4

2. find out the smallest index from the map in step 1 (a - 2);

3. **the first letter in the final result must be the smallest letter from index 0 to index 2;**

4. repeat step 2 to 3 to find out remaining letters.

   - the smallest letter from index 0 to index 2: a

   - the smallest letter from index 3 to index 4: c

   - the smallest letter from index 4 to index 4: d

   - the smallest letter from index 5 to index 6: b

```java

class Solution {

    public String removeDuplicateLetters(String s) {
        if (s.length() == 0)
            return "";
        Map<Character, Integer> map = new HashMap<>();

        for (int index = 0; index < s.length(); index++) {
            map.put(s.charAt(index), index);
        }

        int index = findSmallestIndex(map);
        char c = findSmallestChar(s, index);
        int smallestIndex = findFirstCharIndex(s, c);
        return c + removeDuplicateLetters(s.substring(smallestIndex).replaceAll(c+"", ""));
    }

    private int findSmallestIndex(Map<Character, Integer> map) {
        int res = Integer.MAX_VALUE;
        for (int index : map.values()) {
            if (res > index)
                res = index;
        }
        return res;
    }

    private char findSmallestChar(String s, int endIndex) {
        char res = 'z';
        for (int i=0; i <= endIndex; i++) {
            if (res > s.charAt(i))
                res = s.charAt(i);
        }
        return res;
    }

    private int findFirstCharIndex(String s, char c) {
        for (int index=0; index < s.length(); index++) {
            if (c == s.charAt(index))
                return index;
        }
        return 0;
    }
}
```

