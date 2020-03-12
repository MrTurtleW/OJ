# 自己写的

递归

```java
class Solution {
    private List<Integer> result = new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        if (root == null)
            return result;
        
        result.add(root.val);
        preorderTraversal(root.left);
        preorderTraversal(root.right);
        return result;
    }
}
```

循环

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        TreeNode current = root;

        while (current != null || !stack.isEmpty()) {
            if (current != null){
                result.add(current.val);
                stack.push(current.right);
                stack.push(current.left);
            }
            current = stack.pop();
        }
        return result;
    }
}
```