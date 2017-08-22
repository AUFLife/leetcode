### 104. Maximum Depth of Binary Tree

Difficulty : **Easy**



Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Solution:**

Python

```
def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        from collections import deque
        queue = deque([root, 1])
        while queue:
            node, val = queue.popleft()
            if not node.left and not node.right and not queue:
                return val
            if node.left:
                queue.append((node.left, val + 1))
            if node.right:
                queue.append((node.right, val + 1))
```

Scala

```

```

 Java

```
/**
 * DFS(Deep First Search)
 * @param root
 * @return
 */
public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Stack<TreeNode> stack = new Stack<>();  // 存储树的节点，通过入栈出栈表示是否访问过节点
        Stack<Integer> value = new Stack<>();   // 用于存储当前节点所处深度
        stack.push(root);                       // 根节点入栈
        value.push(1);                    // 当前深度为1
        int max = 0;
        while (!stack.isEmpty()) {              // 如果栈中非空则循
            TreeNode node = stack.pop();        // 从栈顶获取一个元素
            int temp = value.pop();             // 从栈顶获取当前深度
            max = Math.max(temp, max);          // max用来记录当前最大深度
            if (node.left != null) {            // 如果左节点非空，将该节点入栈，存储当前节点已知左节点深度 + 1（）
                stack.push(node.left);
                value.push(temp + 1);
            }
            if (node.right != null) {           // 如果当前节点右节点非空
                stack.push(node.right);         // 右节点入栈
                value.push(temp + 1);     // 深度 + 1
            }
        }
        return max;
    }
```



