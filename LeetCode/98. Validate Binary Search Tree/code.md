# 题解

两种思路
1. 递归判断
2. 二叉搜索树中序遍历有序


递归（自己写的）：
- 也是利用中序遍历有序的思想
- 保存中序遍历上一个值来判断是否有序

```java
class Solution {
    // 用来保存中序遍历上一个值是否有序
    private TreeNode lastVal = null;
    public boolean isValidBST(TreeNode root) {
        if (root == null)
            return true;
        if (!isValidBST(root.left))
            return false;
        if (lastVal == null)
            lastVal = root;
        else if (root.val > lastVal.val) {
            lastVal = root;
        }
        else {
            return false;
        }
        return isValidBST(root.right);
    }
}
```

中序遍历：

```java
public boolean isValidBST(TreeNode root) {
   if (root == null) return true;
   Stack<TreeNode> stack = new Stack<>();
   TreeNode pre = null;
   while (root != null || !stack.isEmpty()) {
      while (root != null) {
         stack.push(root);
         root = root.left;
      }
      root = stack.pop();
      if(pre != null && root.val <= pre.val) return false;
      pre = root;
      root = root.right;
   }
   return true;
}
```