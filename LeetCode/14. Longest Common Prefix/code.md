```java
class Solution {
    private String strs[];
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0)
            return "";
        this.strs = strs;
        int maxLength = 0;
        boolean equal = true;

        while (equal = checkEqual(maxLength))
            maxLength++;
        return strs[0].substring(0, maxLength);
    }

    private boolean checkEqual(int index) {
        char c = ' ';
        for (String str: strs) {
            if (index >= str.length())
                return false;
            else if (c == ' ') {
                c = str.charAt(index);
            }
            else if (c != str.charAt(index))
                return false;
        }
        return true;
    }
}
```

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }

       int index = 0;

       while (true) {
           if (strs[0].length() <= index)
               return strs[0].substring(0, index);

           char c = strs[0].charAt(index);

           for (String s: strs) {
               if (s.length() <= index || s.charAt(index) != c)
                   return strs[0].substring(0, index);
           }
           index++;
       }
    }
}
```

