```java
class Solution {
    public double myPow(double x, int n) {
        if (n == 0)
            return 1;
        
        if (x == 1)
            return 1;
        double res = x;
        for (int i = 1; i < Math.abs(n); i++) {
            res *= x;
        }
        if (n < 0)
            res = 1 / res;
        return res;
    }
}
```