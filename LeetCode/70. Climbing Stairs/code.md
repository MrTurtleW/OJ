# 自己写的

斐波那契书列

```java
class Solution {
    public int climbStairs(int n) {
        int i_1 = 1;
        int i_2 = 1;
        int temp;
        int i = 2;
        while(i <= n){
            temp = i_1 + i_2;
            i_1 = i_2;
            i_2 = temp;
            i++;
        }
        return i_2;
    }
}
```