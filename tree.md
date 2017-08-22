### 104. Maximum Depth of Binary Tree

Difficulty : **Easy**

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

解题思路：递归（Recursion）

**Solution:**

Python

```
def mergeTrees(self, t1, t2):
        """
        :type t1: TreeNode
        :type t2: TreeNode
        :rtype: TreeNode
        """
        if t1 and t2:
            root = TreeNode(t1.val + t2.val)
            root.left = self.mergeTrees(t1.left, t1.right)
            root.right = self.mergeTrees(t1.right, t2.right)
            return root
        else:
            return t1 or t2
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



