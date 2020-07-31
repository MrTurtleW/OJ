```java
class Solution {
    public String countAndSay(int n) {
        if (n == 1)
            return "1";
        String current = "1";
        for (int i = 2; i <= n; i++) {
            current = get_next(current);
        }
        return current;
    }

    private String get_next(String str) {
        StringBuilder builder = new StringBuilder();
        int index = 0;
        while (index < str.length()) {
            char current = str.charAt(index);
            index++;
            int count = 1;
            while (index < str.length() && str.charAt(index) == current) {
                index++;
                count++;
            }
            builder.append(count).append(current);
        }
        return builder.toString();
    }
}
```