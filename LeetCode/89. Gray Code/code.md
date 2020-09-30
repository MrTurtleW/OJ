```java
import java.util.*;

class Solution {
    char[] ch;
    List<Integer> result = new LinkedList<>();
    Map<Character, Character> map = new HashMap<>();
    public List<Integer> grayCode(int n) {
        ch = new char[n];

        Arrays.fill(ch, '0');
        map.put('0', '1');
        map.put('1', '0');
        helper();

        return result;
    }

    public void helper() {
        int converted = arrayToInt();
        if (result.contains(converted)) {
            return;
        }
        result.add(converted);
        for (int i = 0; i < ch.length; i++) {
            ch[i] = map.get(ch[i]);
            helper();
            ch[i] = map.get(ch[i]);
        }
    }

    private int arrayToInt() {
        int res = 0;
        for (char c: ch) {
            res *= 2;
            if (c == '1')
                res += 1;
        }
        return res;
    }
}
```

