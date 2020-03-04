# 自己写的

暴力：先列举前几个

第三个台阶要么从第二个台阶上，要么从第一个台阶上。

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

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.climbStairs(5));
    }
}
```