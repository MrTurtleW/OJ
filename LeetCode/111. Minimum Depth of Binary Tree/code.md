# 题解

```java
public class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        int left = minDepth(root.left);
        int right = minDepth(root.right);
        return (left == 0 || right == 0) ? left + right + 1: Math.min(left,right) + 1;
       
    }
}
```

```java
public static int minDepth(TreeNode root) {
	if (root == null)	return 0;
	if (root.left == null)	return minDepth(root.right) + 1;
	if (root.right == null) return minDepth(root.left) + 1;
	return Math.min(minDepth(root.left),minDepth(root.right)) + 1;
}
```

迭代

```java
public int minDepth(TreeNode root) {
    if(root == null)
        return 0;
    Queue<TreeNode> que = new LinkedList();
    int level = 1;
    que.add(root);
    while(!que.isEmpty()){
        int size = que.size();
        while(size>0){
            TreeNode node =que.poll();
            if(node.left == null && node.right ==null)
                return level;
            if(node.left != null)
                que.add(node.left);
            if(node.right != null)
                que.add(node.right);
            size--;
        }
        level++;
    }
    return level;
}
```