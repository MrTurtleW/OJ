```java
class Solution {
    public String convert(String s, int numRows) {
        if (s.length() < 2)
            return s;
        if (numRows == 1)
            return s;
        StringBuilder[] builders = new StringBuilder[numRows];

        for (int i = 0; i < numRows; i++) {
            builders[i] = new StringBuilder();
        }

        int total = 2 * (numRows - 1);
        for (int i = 0; i < s.length(); i++) {
            int loc = i % total;
            if (loc >= numRows)
                loc = total - loc;
            builders[loc].append(s.charAt(i));
        }

        for (int i = 1; i < numRows; i++) {
            builders[0].append(builders[i]);
        }
        return builders[0].toString();
    }
}
```

```java
class Solution {
    public String convert(String s, int numRows) {
        if (s.length() < 2)
            return s;
        if (numRows == 1)
            return s;

        int total = 2 * (numRows - 1);
        StringBuilder builder = new StringBuilder();
        for (int i = 0; i < numRows; i++) {
            int current = 0;
            while (current + i < s.length()) {
                builder.append(s.charAt(current + i));
                if (i != 0 && i != numRows - 1 && current + total - i < s.length())
                    builder.append(s.charAt(current + total - i));
                current += total;
            }
        }
        return builder.toString();
    }
}
```