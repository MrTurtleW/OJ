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