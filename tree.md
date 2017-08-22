### 104. Maximum Depth of Binary Tree

Difficulty : **Easy**



Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

解题思路：递归（Recursion）

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
def mergeTrees(t1: TreeNode, t2: TreeNode): TreeNode = {
    if (t1 == null && t2 == null) return null
    else if (t1 == null) return t2
    else if (t2 == null) return t1
    val n = new TreeNode(t1.value + t2.value)

    n.left = mergeTrees(t1.left, t2.left)
    n.right = mergeTrees(t1.right, t2.right)
    n
}
```

Java

```
private TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return null;
        else if (t1 == null) return t2;
        else if ( t2 == null) return t1;

        TreeNode n = new TreeNode(t1.val + t2.val);
        n.left = mergeTrees(t1.left, t2.left);
        n.right = mergeTrees(t1.right, t2.right);
        return n;
}
```



