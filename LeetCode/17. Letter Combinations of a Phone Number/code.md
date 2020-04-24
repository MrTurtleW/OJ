```java
import java.util.*;

class Solution {

    private Map<Character, String> map;

    private List<String> ans;
    private String digits;

    public Solution() {
        ans = new ArrayList<>();

        map = new HashMap<>();
        map.put('2', "abc");
        map.put('3', "def");
        map.put('4', "ghi");
        map.put('5', "jkl");
        map.put('6', "mno");
        map.put('7', "pqrs");
        map.put('8', "tuv");
        map.put('9', "wxyz");
    }
    public List<String> letterCombinations(String digits) {
        if (digits.length() > 0) {
            this.digits = digits;
            helper("");
        }
        return ans;
    }

    private void helper(String tempResult) {
        if (tempResult.length() == digits.length()) {
            ans.add(tempResult);
            return;
        }

        char currentChar = digits.charAt(tempResult.length());
        for (int i=0; i< map.get(currentChar).length(); i++) {
            helper(tempResult + map.get(currentChar).charAt(i));
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.letterCombinations("23"));
    }
}
```