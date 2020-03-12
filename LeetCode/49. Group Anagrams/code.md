# 自己写的

## 暴力解法

排序，看是否相等

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;

class Solution {

    private String[] sorted;

    List<List<String>> result;

    private String charArrayToString(char[] charArray) {
        StringBuilder builder = new StringBuilder();
        for(char c: charArray) {
            builder.append(c);
        }
        return builder.toString();
    }

    private int existsStringIndex(String target) {
        for (int i = 0; i < result.size(); i++) {
            if (sorted[i].equals(target))
                return i;
        }
        return -1;
    }

    public List<List<String>> groupAnagrams(String[] strs) {
        result = new LinkedList<List<String>>();

        sorted = new String[strs.length];

        for (int i = 0; i < strs.length; i++) {
            char[] charArr = strs[i].toCharArray();
            Arrays.sort(charArr);
            // 判断是否有相等的
            int index = existsStringIndex(charArrayToString(charArr));
            if (index >= 0) {
                result.get(index).add(strs[i]);
            }
            else {
                List<String> list = new ArrayList<String>();
                list.add(strs[i]);
                result.add(list);
                sorted[result.size()-1] = charArrayToString(charArr);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String[] strs = {"eat", "tea", "tan", "ate", "nat", ""};
        Solution solution = new Solution();
        System.out.println(solution.groupAnagrams(strs));
    }
}
```

## 利用数组

```java
import java.util.*;

class Solution {

    List<List<String>> result;

    private boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        int [] a = new int [26];
        for(Character c : s.toCharArray()) a[c - 'a']++;
        for(Character c : t.toCharArray()) {
            if(a[c -'a'] == 0) return false;
            a[c - 'a']--;
        }
        return true;
    }

    public void findAnagram(String s) {

        for (List<String> group : result) {
            if (isAnagram(group.get(0), s)) {
                group.add(s);
                return;
            }
        }
        List<String> group = new ArrayList<String>();
        group.add(s);
        result.add(group);
    }

    public List<List<String>> groupAnagrams(String[] strs) {
        result = new LinkedList<List<String>>();

        for (String s: strs) {
            findAnagram(s);
        }
        return result;
    }

    public static void main(String[] args) {
        String[] strs = {"eat", "tea", "tan", "ate", "nat", ""};
        Solution solution = new Solution();
        System.out.println(solution.groupAnagrams(strs));
    }
}
```

### 把排序后的值作为key，然后归类输出

```java
import java.util.*;

class Solution {

    private String charArrayToString(char[] charArray) {
        StringBuilder builder = new StringBuilder();
        for(char c: charArray) {
            builder.append(c);
        }
        return builder.toString();
    }

    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new LinkedList<List<String>>();

        Map<String, Integer> hash = new HashMap<String, Integer>();

        for (String str : strs) {
            char[] charArr = str.toCharArray();
            Arrays.sort(charArr);
            String sorted = charArrayToString(charArr);
            if (hash.containsKey(sorted)) {
                result.get(hash.get(sorted)).add(str);
            }
            else {
                List<String> group = new ArrayList<String>();
                group.add(str);
                result.add(group);
                hash.put(sorted, result.size()-1);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        String[] strs = {"eat", "tea", "tan", "ate", "nat", ""};
        Solution solution = new Solution();
        System.out.println(solution.groupAnagrams(strs));
    }
}
```

速度非常快