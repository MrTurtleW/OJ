```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;


class Solution {
    private String s;
    private int index = 0;
    private List<String> list;
    public int romanToInt(String s) {
        this.s = s;
        list =  Arrays.asList("IV","IX", "XL", "XC", "CD", "CM");

        int[] value = {    1,   4,    5,   9,    10,  40,   50,  90,   100, 400,  500, 900,  1000};
        String[] symbols = {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};

        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < value.length; i++) {
            map.put(symbols[i], value[i]);
        }

        String symbol = "";
        int res = 0;

        while (!(symbol = getNextSymbol()).equals("")) {
            res += map.get(symbol);
        }
        return res;
    }

    private String getNextSymbol() {
        String res = "";

        if (index < s.length() - 1 && list.contains(s.substring(index, index+2))) {
            res = s.substring(index, index+2);
            index += 2;
        }
        else if (index < s.length()){
            res = s.substring(index, index+1);
            index += 1;
        }
        return res;
    }
}
```