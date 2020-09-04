```java
class Solution {
    public String addBinary(String a, String b) {
        int carry = 0;
        int aIndex = a.length() - 1, bIndex = b.length() - 1;

        StringBuilder builder = new StringBuilder();

        while (caption > 0 || aIndex >= 0 || bIndex >= 0) {
            int aInt = 0, bInt = 0;
            if (aIndex >= 0) {
               aInt = a.charAt(aIndex) == '1' ? 1 : 0;
               aIndex--;
            }

            if (bIndex >= 0) {
                bInt = b.charAt(bIndex) == '1' ? 1 : 0;
                bIndex --;
            }

            int result = aInt + bInt + carry;

            if (result >= 2) {
                carry = 1;
                result -= 2;
            }
            else {
                carry = 0;
            }

            builder.insert(0, result);
        }

        return builder.toString();
    }
}
```

