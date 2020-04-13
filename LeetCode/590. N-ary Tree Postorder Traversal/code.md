# 自己写的

```java
class Solution {
    private List<Integer> result = new ArrayList<>();
    public List<Integer> postorder(Node root) {
        if (root == null)
            return result;
        for(Node node: root.children) {
            postorder(node);
        }
        result.add(root.val);
        return result;
    }
}
```

# 题解

循环

```java
class Solution {
    public List<Integer> postorder(Node root) {
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
        // 可以直接使用 LinkedList，每次插入前面
        Collections.reverse(list);
        return list;
    }
}
```