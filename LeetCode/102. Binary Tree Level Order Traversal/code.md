```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();

        if (root == null)
            return res;

        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> temp = new ArrayList<>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                temp.add(node.val);
                if (node.left != null)
                    queue.offer(node.left);
                if (node.right != null)
                    queue.offer(node.right);
            }
            res.add(temp);
        }

        return res;
    }
}
```

深度优先遍历：

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

class Solution {
    Set<TreeNode> set = new HashSet<>();
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {

        dfs(root, 0);

        return res;
    }
    private void dfs(TreeNode node, int level) {
        if (node == null)
            return;
        if (set.contains(node))
            return;

        while (res.size() <= level)
            res.add(new ArrayList<>());

        res.get(level).add(node.val);
        if (node.left != null) {
            dfs(node.left, level+1);
        }
        if (node.right != null) {
            dfs(node.right, level+1);
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        TreeNode root = new TreeNode(3);
        root.left = new TreeNode(9);
        root.right = new TreeNode(20);
        root.right.left = new TreeNode(15);
        root.right.right = new TreeNode(7);
        System.out.println(solution.levelOrder(root));
    }
}
```


# 2020-04-28

BFS

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if root is None:
            return []

        res = []
        queue = [root]

        while queue:
            temp = []
            size = len(queue)
            for i in range(size):
                temp.append(queue[0].val)
                if queue[0].left:
                    queue.append(queue[0].left)
                if queue[0].right:
                    queue.append(queue[0].right)

                del queue[0]

            res.append(temp)

        return res
```