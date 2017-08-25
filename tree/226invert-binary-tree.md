### 226. Invert Binary Tree

Difficulty : **Easy**

Invert a binary tree.

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

to

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**Trivia:**

This problem was inspired by [this original tweet](https://twitter.com/mxcl/status/608682016205344768) by [Max Howell](https://twitter.com/mxcl):

> Google: 90% of our engineers use the software you wrote \(Homebrew\), but you can’t invert a binary tree on a whiteboard so fuck off.

**Solution:**

Python

```py
def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        queue = collections.deque([root])
        while queue:
            node = queue.popleft()
            if node:
                node.left, node.right = node.right, node.left
                queue.append(node.left)
                queue.append(node.right)
        return root
```

Scala

```Scala
/**
    * BFS
    * Non-Recursion: 类似二叉树层序遍历，需要用queue来辅助，先把根节点排入队列中，然后从队列中取出来，交换其左右节点，如果存在则分别
    * 将 左右节点再排入队列中，依次类推直到队列中木有节点了停止循环，返回root即可。
    *
    * @param root
    * @return
    */
  def invertTree(root: TreeNode): TreeNode = {
    if (root == null) return null
    val queue = new Queue[TreeNode]()
    queue += root // 根节点入队列

    while (queue.nonEmpty) {
      val node = queue.dequeue()
      val left = node.left
      node.left = node.right
      node.right = left
      if (node.left != null) queue += node.left
      if (node.right != null) queue += node.right
    }
    return root
  }
```

Java

```
/**
 * DFS
 */
public TreeNode invertTree(TreeNode root) {
        
        if (root == null) {
            return null;
        }

        final Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        
        while(!stack.isEmpty()) {
            final TreeNode node = stack.pop();
            final TreeNode left = node.left;
            node.left = node.right;
            node.right = left;
            
            if(node.left != null) {
                stack.push(node.left);
            }
            if(node.right != null) {
                stack.push(node.right);
            }
        }
        return root;
    }
```



