```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int index = 0;
        int start = newInterval[0], end = newInterval[1];

        List<int[]> result = new ArrayList<>();

        while (index < intervals.length && intervals[index][1] < start)
            result.add(intervals[index++]);

        while (index < intervals.length && intervals[index][0] <= end) {
            start = Math.min(start, intervals[index][0]);
            end = Math.max(end, intervals[index++][1]);
        }
        result.add(new int[]{start, end});

        while (index < intervals.length)
            result.add(intervals[index++]);

        return result.toArray(new int[result.size()][]);
    }
}
```

