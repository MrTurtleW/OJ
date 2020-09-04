```java
class Solution {
    public int mySqrt(int x) {
        if (x == 1)
            return 1;
        long num = x / 2;
        while (true) {
            if (num * num > x)
                num /= 2;
            else if ((num+1) * (num+1) <= x)
                num++;
            else
                return (int)num;
        }

    }
}
```

