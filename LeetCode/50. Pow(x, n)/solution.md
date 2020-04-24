# 分治

`$2^{10}=2^5*2^5, 2^5= (2^2)*2$`

时间复杂度为`$O(\log n)$`

```java
class Solution {
    public double myPow(double x, int n) {
        double res = 0;
        double subResult;
        if (n < 0) {
            res = 1 / myPow(x, -n);
        }
        else if (n == 0)
            res = 1;

        else if (n % 2 == 0) {
            subResult = myPow(x, n / 2);
            res =  subResult * subResult;
        }
        else {
            subResult = myPow(x, n / 2);
            res =  subResult * subResult * x;
        }
        return res;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.myPow(2, -2147483648));
    }
}
```

对于`Integer.MIN_VALUE`报StackOverFlow

```java
class Solution {
    public double myPow(double x, int n) {
        if(n == 0)
            return 1;
        if(n<0){
            return 1/x * myPow(1/x, -(n + 1));
        }
        return (n%2 == 0) ? myPow(x*x, n/2) : x*myPow(x*x, n/2);
    }
}
```

# 快速幂

假设求`$a^b$`，把b写成它的二进制形式，设该二进制数第i位的权值为`$2^{(i-1)}$`，`$i * 2^{(i-1) }$`是每一次要做的乘方次数那么假设b=11，11的二进制是1011，则

```math
a^b = a^{2^0}*a^{2^1}*a^{2^2}
```

```java
class Solution {
    public double myPow(double x, int n) {
        boolean negative = n < 0;
        double res = 1;
        while (n != 0) {
            if ((n & 1) != 0) {
                // n的最后一位
                res *= x;
            }
            x *= x;
            n /= 2;
        }
        return negative ? 1 / res : res;
    }
}
```