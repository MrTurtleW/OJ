```java
class Solution {
    String s1, s2, s3;
    public boolean isInterleave(String s1, String s2, String s3) {
        this.s1 = s1;
        this.s2 = s2;
        this.s3 = s3;
        return helper(0, 0, 0);
    }

    boolean helper(int i, int j, int k) {
        if (i == s1.length() && j == s2.length() && k == s3.length())
            return true;
        if (k >= s3.length())
            return false;
        if (i < s1.length() && s1.charAt(i) == s3.charAt(k) && helper(i + 1, j, k + 1)) {
            return true;
        }
        return j < s2.length() && s2.charAt(j) == s3.charAt(k) && helper(i, j + 1, k + 1);
    }
}
```

