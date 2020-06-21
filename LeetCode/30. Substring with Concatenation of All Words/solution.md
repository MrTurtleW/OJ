```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new LinkedList<>();
        if (s.length() == 0 || words.length == 0 || words[0].length() == 0)
            return res;

        Map<String, Integer> counts = new HashMap<>();
        for (String word: words) {
            counts.put(word, counts.getOrDefault(word, 0) + 1);
        }

        int wordLength = words[0].length(), numOfWords = words.length;
        for (int i = 0; i <= s.length() - wordLength * numOfWords ; i++) {
            Map<String, Integer> seen = new HashMap<>();

            for (int j = 0; j < numOfWords; j++) {
                String subStr = s.substring(i + j * wordLength, i + (j+1) * wordLength);
                
                if (!counts.containsKey(subStr))
                    break;
                seen.put(subStr, seen.getOrDefault(subStr, 0) + 1);

                if (seen.get(subStr) > counts.get(subStr))
                    break;

                if (j == numOfWords-1)
                    res.add(i);
            }
        }
        return res;
    }
}
```