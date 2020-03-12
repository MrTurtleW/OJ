# 自己写的

层次遍历，记录层数

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null)
            return 0;

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        int height = 0;

        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null)
                    queue.offer(node.left);
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            height += 1;
        }
        return height;
    }
}
```

# 题解

```java
public class Solution {
    public int maxDepth(TreeNode root) {
        return root==null? 0 : Math.max(maxDepth(root.left), maxDepth(root.right))+1;
    }
}
```