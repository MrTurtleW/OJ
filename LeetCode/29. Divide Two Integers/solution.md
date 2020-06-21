```java
class Solution {
    public int divide(int A, int B) {
        if (A == Integer.MIN_VALUE && B == -1) return Integer.MAX_VALUE;
        int a = Math.abs(A), b = Math.abs(B), res = 0, x = 0;
        // 不能写成 a >= b，对于 A = Integer.MIN_VALUE, B = 1，a-b溢出
        while (a - b >= 0) {
            for (x = 0; a - (b << x << 1) >= 0; x++);
            res += 1 << x;
            a -= b << x;
        }
        return (A > 0) == (B > 0) ? res : -res;
    }
}
```