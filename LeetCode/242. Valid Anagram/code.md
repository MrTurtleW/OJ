# 自己写的

- 暴力，sort后挨个比较
- 哈希表

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length())
            return false;
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (char c: s.toCharArray()) {
            if (!map.containsKey(c)) {
                map.put(c, 1);
            }
            else {
                map.put(c, map.get(c) + 1);
            }
        }

        for (char c: t.toCharArray()) {
            if (!map.containsKey(c))
                return false;
            map.put(c, map.get(c)-1);
            if (map.get(c) == 0) {
                map.remove(c);
            }
        }
        if (!map.isEmpty())
            return false;
        return true;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String s = "anagram", t = "nagaram";
        System.out.println(solution.isAnagram(s, t));
    }
}
```

# 题解

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        int [] a = new int [26];
        for(Character c : s.toCharArray()) a[c - 'a']++;
        for(Character c : t.toCharArray()) {
            if(a[c -'a'] == 0) return false;
            a[c - 'a']--;
        }
        return true;
    }
}
```