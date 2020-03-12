# 自己写的
递归

```java
class Solution {
    private List<Integer> result = new ArrayList<>();
    public List<Integer> preorder(Node root) {
        if (root == null)
            return result;

        result.add(root.val);
        for(Node node: root.children) {
            preorder(node);
        }
        return result;
    }
}
```

循环

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) return list;
        
        Stack<Node> stack = new Stack<>();
        stack.add(root);
        
        while(!stack.isEmpty()) {
            root = stack.pop();
            list.add(root.val);
            for(Node node: root.children)
                stack.add(node);
        }
        return list;
    }
}
```