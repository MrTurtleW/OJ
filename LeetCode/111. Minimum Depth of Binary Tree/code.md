# 题解

```java
public static int minDepth(TreeNode root) {
	if (root == null)	return 0;
	if (root.left == null)	return minDepth(root.right) + 1;
	if (root.right == null) return minDepth(root.left) + 1;
	return Math.min(minDepth(root.left),minDepth(root.right)) + 1;
}
```

迭代（层次遍历第一个叶子节点的高度就是最小高度）

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
            // 层次遍历达到叶子节点，则找到最小高度
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