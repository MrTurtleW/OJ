```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> result = new LinkedList<>();

        List<String> temp = new LinkedList<>();
        helper(result, s, temp, 0);
        return result;
    }

    void helper(List<String> result, String s, List<String> temp, int index) {
        if (temp.size() == 4) {
            if (index == s.length())
                result.add(String.join(".", temp));
            return;
        }


        if (index >= s.length())
            return;

        // 1位
        temp.add(s.substring(index, index+1));
        helper(result, s, temp, index+1);
        temp.remove(temp.size()-1);
        // 2位
        if (s.charAt(index) != '0' && index < s.length() - 1) {
            temp.add(s.substring(index, index+2));
            helper(result, s, temp, index+2);
            temp.remove(temp.size()-1);
        }
        // 3位
        if (s.charAt(index) != '0' && index < s.length() - 2 && (s.charAt(index) == '1' || (s.charAt(index) == '2' && s.charAt(index+1) < '5') || (s.charAt(index) == '2' && s.charAt(index+1) == '5' && s.charAt(index+2) <= '5'))) {
            temp.add( s.substring(index, index+3));
            helper(result, s, temp, index+3);
            temp.remove(temp.size()-1);
        }
    }
}
```

