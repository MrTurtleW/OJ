动态规划：

```java
class Solution {
    public int longestValidParentheses(String s) {
        int[] dp = new int[s.length()];

        int max = 0, open = 0;
        for (int i=0; i < s.length(); i++) {
            if (s.charAt(i) == '(')
                open++;
            else if (open > 0) {
                dp[i] = 2 + dp[i-1];
                if (i > dp[i])
                    dp[i] += dp[i-dp[i]];
                open--;
            }
            max = Math.max(dp[i], max);
        }
        return max;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.longestValidParentheses(")()())"));
    }
}
```

栈：

```java
class Solution {
    public int longestValidParentheses(String s) {
        int longest = 0;
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            // if we met (, push the index into stack
            // if we met ), and top of stack is (, we found a match, pop ( from stack
            if (s.charAt(i) == ')' && !stack.isEmpty() && s.charAt(stack.peek()) == '(')
                stack.pop();
            else
                stack.push(i);
        }

        // After the scan is done, the stack will only
        // contain the indices of characters which cannot be matched. Then
        // let's use the opposite side - substring between adjacent indices
        // should be valid parentheses.
        if (stack.isEmpty())
            longest = s.length();
        else {
            int a = s.length(), b = 0;
            while (!stack.isEmpty()) {
                b = stack.pop();
                longest = Math.max(longest, a-b-1);
                a = b;
            }
            longest = Math.max(longest, a);
        }
        return longest;
    }
}
```