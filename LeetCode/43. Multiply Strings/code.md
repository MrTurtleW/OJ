```java
class Solution {
    public String multiply(String num1, String num2) {
        String result = "";
        if (num1.length() == 0 || num2.length() == 0)
            return result;
        
        if (num1.equals("0") || num2.equals("0"))
            return "0";

        for (char c: num1.toCharArray()) {
            result = add(multiplySingle(result, 10), multiplySingle(num2, c-'0'));
        }
        return result;
    }

    public String multiplySingle(String s, int n) {
        int i = s.length() - 1, caption = 0, sum=0;
        StringBuilder result = new StringBuilder();
        while (i >= 0) {
            sum = (s.charAt(i) - '0') * n + caption;
            caption = sum / 10;
            result.insert(0, sum - caption * 10);
            i--;
        }
        if (caption > 0)
            result.insert(0, caption);
        return result.toString();
    }

    public String add(String s1, String s2) {
        int i = s1.length()-1, j=s2.length()-1, caption=0, sum=0;
        StringBuilder builder = new StringBuilder();
        while (i >=0 || j >=0) {
            int left = 0, right=0;
            if (i < 0)
                left = 0;
            else {
                left = s1.charAt(i) - '0';
                i--;
            }

            if (j < 0)
                right = 0;
            else {
                right = s2.charAt(j) - '0';
                j--;
            }
            sum = left + right + caption;
            caption = sum / 10;
            builder.insert(0, sum - caption * 10);
        }
        if (caption > 0) {
            builder.insert(0, caption);
        }
        return builder.toString();
    }
}
```