```java
class Solution {
    private String haystack;
    private String needle;
    public int strStr(String haystack, String needle) {
        if (haystack.length() == 0 && needle.length() == 0)
            return 0;
        
        if (haystack.length() < needle.length())
            return -1;

        this.haystack = haystack;
        this.needle = needle;

        for (int i = 0; i <= haystack.length()-needle.length(); i++) {
            if (check(i))
                return i;
        }
        return -1;
    }

    private boolean check(int index) {
        for (int i = 0; i < needle.length(); i++) {
            if (i + index >= haystack.length())
                return false;
            if (haystack.charAt(i+index) != needle.charAt(i))
                return false;
        }
        return true;
    }
}
```