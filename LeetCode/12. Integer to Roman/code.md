```java
class Solution {

    StringBuilder builder = new StringBuilder();
    int[] value = {    1,   4,    5,   9,    10,  40,   50,  90,   100, 400,  500, 900,  1000};
    String[] symbol = {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};

    public String intToRoman(int num) {
        helper(num, value.length-1);
        return builder.toString();
    }

    private void helper(int num, int index) {
        if (index < 0)
            return;

        while (num >= value[index]) {
            builder.append(symbol[index]);
            num -= value[index];
        }

        helper(num, --index);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.intToRoman(1994));
    }
}
```