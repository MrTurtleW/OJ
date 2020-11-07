# DP

Given a sequence `1..n` to construct a Binary Search Tree out of the sequence, we could enumerate each number `i` in the sequence, and use the number as the root, naturally, the subsequence `1...(i-1)` on its left side would lay on the left branch of the root, and similarly the right subsequence `(i+1)..n` lay on the right branch of the root. We then can construct the subtree from the subsequence recursively. 

Through the above approach, we could ensure that the BST that we construct are all unique, since they have unique roots.

The problem is to calculate the number of unique BST. To do so, we need to define two functions:

- `G(n)`: the number of unique BST for a seqence of length `n`
- `F(i, n), i <= i <= n`: the number of unique BST, where the number `i` is the root of BST, and the sequence ranges from `1` to `n`

We can see that the total number of unique BST `G(n)`, is the sum of BST `F(i)` using each number `i` as a root:
$$
G(n)=F(1,n) +F(2,n)+\cdots+F(n,n)
$$
Particularly, 

- $G(0)=1$
- $G(1)=1$

Given a sequence `1...n`, we pick a number `i` out of the sequence as the root, then the number of unique BST with the specified root `F(i)`, is the cartesian product （笛卡尔积）of the number of BST for its left and right subtrees.

> For example, $F(3, 7)$: the number of unique BST tree with number 3 as its root. To construct an unique BST out of the entire sequence `[1,2,3,4,5,6,7]` with 3 as the root, which is to say, we need to construct an unique BST out of its left subsequence `[1,2]` and another BST out of the right subsequence `[4,5,6,7]`, and then combine them together. 
>
> We could consider the number of unique BST out of sequence `[1,2]` as $G(2)$, and the number of unique BST out of sequence `[4,5,6,7]` as $G(4)$. Therefore, $F(3,7)=G(2)*G(4)$
>
> So
> $$
> F(i,n)=G(i-1)*G(n-i)
> $$

Combining the above formulas, we obtain the recursive formula for $G(n)$
$$
G(n)=G(0)*G(n-1) +G(1)*G(n-2)+\cdots+G(n-1)*G(0)
$$

```java
class Solution {
    public int numTrees(int n) {
        int [] G = new int[n+1];
        G[0] = G[1] = 1;

        for(int i=2; i<=n; ++i) {
            for(int j=1; j<=i; ++j) {
                G[i] += G[j-1] * G[i-j];
            }
        }
        return G[n];
    }
}
```

# 卡特兰数

卡特兰数是组合数学中的一种著名数列，通常用如下通项式表示：
$$
f(n)=\frac{C_{2n}^n}{n+1}
$$
递推式：
$$
f(n)=\sum_{i=0}^{n-1}f(i)\times f(n-i-1)
$$

实际应用中，最常用的是第一个通项式的变形：
$$
f(n)=C_{2n}^n-C_{2n}^{n-1}
$$