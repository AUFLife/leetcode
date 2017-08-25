转自：[http://www.jianshu.com/p/8c71c3a2b1a2](http://www.jianshu.com/p/8c71c3a2b1a2)

#### 两种算法比较

广度优先搜索一个图的时候是按照树的层次来搜索的，（层次遍历），队列来实现，我们假设一个节点衍生出来的相邻节点的平均个数是N个，那么当起点开始搜索的时候，队列有一个节点，当起点拿出来后，把它相邻的节点放进去，那么队列就有N个节点，当下一层的搜索中再加入元素到队列的时候，节点数达到了N2，你可以想想，一旦N是一个比较大的数的时候，这个树的层次又比较深，那这个队列就得需要很大的内存空间了。  
缺点：在树的层次较深&&子节点个数较多的情况下，消耗内存现象十分严重。因此，BFS适用于节点的子节点个数不多，并且树的层次不会太深的情况。优点：可以得到最优解。

* 与上面相对应的，DFS可以克服这个缺点，因为每次搜索的时候只需要维护一个节点，（递归、栈实现）但回过头想想，广度优先能够找到最短路径，那深度优先能否找到呢？深度优先的方法是一条路走到黑，那显然无法知道这条路是不是最短的，所以你还得继续走别的路去判断是否是最短路。  
  缺点：难以寻找最优解，仅仅只能寻找有解。其优点就是内存消耗小，克服了刚刚说的广度优先搜索的缺点。

一般说来，能用DFS解决的问题都能用BFS解决。DFS通过递归实现，易于实现，DFS的常数时间开销会比较少，所以大多数情况下优先考虑DFS实现。然后就是，DFS容易栈溢出，而BFS可以自己控制队列的长度。最后，BFS加上评估函数可以变成A_算法，DFS加上评估函数可以变成IDA_算法。

### DFS算法

#### 核心思想

它的思想是从一个顶点V0开始，沿着一条路一直走到底，如果发现不能到达目标解，那就返回到上一个节点，然后从另一条路开始走到底，这种尽量往深处走的概念即是深度优先的概念。  
代码表示如下：

```
/**
 * DFS核心伪代码
 * 前置条件是visit数组全部设置成false
 * @param n 当前开始搜索的节点
 * @param d 当前到达的深度
 * @return 是否有解
 */
bool DFS(Node n, int d){
    if (isEnd(n, d)){//一旦搜索深度到达一个结束状态，就返回true
        return true;
    }

    for (Node nextNode in n){//遍历n相邻的节点nextNode
        if (!visit[nextNode]){//
            visit[nextNode] = true;//在下一步搜索中，nextNode不能再次出现
            if (DFS(nextNode, d+1)){//如果搜索出有解
                //做些其他事情，例如记录结果深度等
                return true;
            }

            //重新设置成false，因为它有可能出现在下一次搜索的别的路径中
            visit[nextNode] = false;
        }
    }
    return false;//本次搜索无解
```

eg.二叉树中和为某一值的路径  
**题目描述**  
输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

```
class Solution {
public:
     vector<vector<int>> res;
     vector<int> path;
    void find(TreeNode* root,  int sum)
    {
        if (root == NULL)return;
        path.push_back(root->val);
        if (!root->left && !root->right && sum == root->val)
            res.push_back(path);
        else
        {
            if (root->left)
                find(root->left, sum - root->val);
            if (root->right)
                find(root->right, sum - root->val);
        }
        path.pop_back();
    }
    vector<vector<int>> FindPath(TreeNode* root,int expectNumber) {
        find(root, expectNumber);
        return res;
    }
};

作者：会发光的二极管
链接：http://www.jianshu.com/p/8c71c3a2b1a2
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

### BFS算法

#### 核心思想

广度优先搜索一个图的时候是按照树的层次来搜索的，（层次遍历），队列来实现，形象的说，这里有点像辐射形状的搜索方式，从一个节点，向其旁边节点传递病毒，就这样一层一层的传递辐射下去，知道目标节点被辐射中了，此时就已经找到了从起点到终点的路径。  
核心代码如下：

```
/**
 * 广度优先搜索
 * @param Vs 起点
 * @param Vd 终点
 */
bool BFS(Node& Vs, Node& Vd){
    queue<Node> Q;
    Node Vn, Vw;
    int i;

    //初始状态将起点放进队列Q
    Q.push(Vs);
    hash(Vw) = true;//设置节点已经访问过了！

    while (!Q.empty()){//队列不为空，继续搜索！
        //取出队列的头Vn
        Vn = Q.front();

        //从队列中移除
        Q.pop();

        while(Vw = Vn通过某规则能够到达的节点){
            if (Vw == Vd){//找到终点了！
                //把路径记录，这里没给出解法
                return true;//返回
            }

            if (isValid(Vw) && !visit[Vw]){
                //Vw是一个合法的节点并且为白色节点
                Q.push(Vw);//加入队列Q
                hash(Vw) = true;//设置节点颜色
            }
        }
    }
    return false;//无解
}

作者：会发光的二极管
链接：http://www.jianshu.com/p/8c71c3a2b1a2
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

对于一个题目来说，要标志节点是否访问过，用数组是一种很快速的方法，但有时数据量太大，很难用一个大数组来记录时，采用hash是最好的做法。实际上visit数组在这里也是充当hash的作用。（PS：至于hash是什么？得自己去了解，它的作用是在O\(1\)的时间复杂度内取出某个值）

### 参考资料

[深度优先算法（DFS）](http://rapheal.iteye.com/blog/1526863)  
[广度优先算法（BFS）](http://blog.csdn.net/raphealguo/article/details/7523411)  
[图的基本算法](http://www.jianshu.com/p/70952b51f0c8)  
[程序员必须知道的十大算法](http://www.jianshu.com/p/c2c4b89aaa4b)  
[图的遍历之DFS&BFS](http://www.cnblogs.com/skywang12345/p/3711483.html)

转自：

作者：会发光的二极管

链接：[http://www.jianshu.com/p/8c71c3a2b1a2](http://www.jianshu.com/p/8c71c3a2b1a2)

