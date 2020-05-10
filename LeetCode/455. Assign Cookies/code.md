```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);

        int i=0, j=0, num=0;
        while (i < g.length && j < s.length) {
            if (s[j] >= g[i]) {
                i++;
                j++;
                num++;
            }
            else {
                j++;
            }
        }
        return num;
    }
}
```

i可以和num用一个变量，j可以用for代替

```java
public class Solution {
    public int findContentChildren(int[] children, int[] cookies) {
        Arrays.sort(children);
        Arrays.sort(cookies);
        
        int child = 0;
        for (int cookie = 0; child < children.length && cookie < cookies.length; cookie ++) {
            if (cookies[cookie] >= children[child]) {
                child ++;
            }
        }
        
        return child;
    }
}
```