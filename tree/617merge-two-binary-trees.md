### 617. Merge Two Binary Trees

Difficulty : **Easy**

Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

**Example 1:**

```
Input: 
    Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
         3
        / \
       4   5
      / \   \ 
     5   4   7
```

**Note:**

The merging process must start from the root nodes of both trees.

**Solution:**

解题思路：递归（Recusion）

Python

```py
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

```java
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



