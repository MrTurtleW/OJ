```java
class Solution {
    public int myAtoi(String str) {

        int index = 0;
        while (index < str.length() && str.charAt(index) == ' ')
            index ++;
        
        if (index >= str.length())
            return 0;

        boolean negative = false;
        if (str.charAt(index) == '+'){
            negative = false;
            index ++;
        }
        else if (str.charAt(index) == '-'){
            index++;
            negative = true;
        }
        else if (str.charAt(index) < '0' && str.charAt(index) > '9')
            return 0;

        int res = 0;
        while (index < str.length() && '0' <= str.charAt(index) &&  str.charAt(index) <= '9') {
            res = res * 10 + str.charAt(index) - '0';

            if (res % 10 != str.charAt(index) - '0') {
                if (negative)
                    return Integer.MIN_VALUE;
                else
                    return Integer.MAX_VALUE;
            }
            index ++;
        }
        if (negative)
            res = -res;
        return res;
    }
}
```