### 338. Counting Bits

Difficulty : **Medium**

Given a non negative integer number**num**. For every numbers**i**in the range**0 ≤ i ≤ num**calculate the number of 1's in their binary representation and return them as an array.

**Example:**  
For`num = 5`you should return`[0,1,1,2,1,2]`.

**Follow up:**

* It is very easy to come up with a solution with run time **O\(n\*sizeof\(integer\)\)**. But can you do it in linear time

  **O\(n\)**/possibly in a single pass?

* Space complexity should be **O\(n\)**

* Can you do it like a boss? Do it without using any builtin function like **\_\_builtin\_popcount **in c++ or in any other language.

**Credits:**  
Special thanks to[@ syedee](https://leetcode.com/discuss/user/syedee)for adding this problem and creating all test cases.

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



