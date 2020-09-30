# 题解

自顶向下编程

```java
import java.util.List;

class Solution {
    public List<String> generateParenthesis(int n) {
        _generate(0, 2 * n, "");
        return null;
    }

    private void _generate(int level, int max, String s) {
        // terminator
        if (level >= max) {
            System.out.println(s);
            return;
        }

        // process current logic

        // drill down
        _generate(level + 1, max, s + "(");
        _generate(level + 1, max, s + ")");

        // reverse states
    }
}
```

接下来只需要去除不合法的序列
- left随时可以加，只要总数不超过n
- right加的时候左边必须有更多的左括号。

因此可以记录已用左括号个数、已用右括号个数和总括号个数：

```java
class Solution {
    List<String> result = new ArrayList<>();
    public List<String> generateParenthesis(int n) {
        _generate(0, 0, n, "");
        return null;
    }

    private void _generate(int left, int right, int n, String s) {
        // terminator
        if (left == right && right == n)
            result.add(s);

        // process current logic

        // drill down
        if (left < n)
            _generate(left + 1, right, n, s + "(");
        if (right < left)
            _generate(left, right + 1, n, s + ")");

        // reverse states
    }
}
```

时间复杂度$O(2^n)$，但进行了剪枝。