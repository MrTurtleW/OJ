# 二分法

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 0)
            return 0;
        int left = 1, right = x / 2 + 1;
        while (true) {
            int mid = left + (right - left)/2;
            if (mid > x/mid) {
                right = mid - 1;
            } else {
                if (mid + 1 > x/(mid + 1))
                    return mid;
                left = mid + 1;
            }
        }
    }
}
```

# 牛顿迭代法

```java
class Solution {
    public int mySqrt(int x) {
        int r = x;
        while (r > x/r)
            r = (r + x/r) / 2;
        return r;
    }
}
```

# 位运算

```java
class Solution {
    public int mySqrt(int x) {
            int ans = 0;
            int bit = 1 << 15;
            while (bit > 0) {
                ans |= bit;
                if (ans > x / ans) {
                    ans ^= bit; 
                }
                bit >>= 1;
            }
            return ans;
        }
}
```

