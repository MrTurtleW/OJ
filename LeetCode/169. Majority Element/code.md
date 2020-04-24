利用map统计出现次数：

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        int maxKey = 0, maxVal = 0;
        for (int num: nums) {
            if (map.containsKey(num)) {
                map.put(num, map.get(num) + 1);
            }
            else {
                map.put(num, 1);
            }
            if (maxVal < map.get(num)) {
                maxKey = num;
                maxVal = map.get(num);
            }
        }
        return maxKey;
    }
}
```