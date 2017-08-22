### 406. Queue Reconstruction by Height

Difficulty : **Medium**



Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers`(h, k)`, where`h`is the height of the person and`k`is the number of people in front of this person who have a height greater than or equal to`h`. Write an algorithm to reconstruct the queue.

**Note:**  
The number of people is less than 1,100.

**Example:**

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

**Soultion:**

1. Pick out tallest group of people and sort them in a subarray\(S\). Since there's no other groups of people taller than them,therefore each guy's index will be just as same as his value.
2. For 2nd tallest group\(and the rest\), insert each one of them into\(S\) by value.So on and so forth.

```
E.g.
* input:[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]
* subarray after step 1:[[7,0],[7,1]]
* subarray after step 2:[[7,0], [7,1]
```



Python

```
    def reconstructQueue(people):
        """
        :param people: List[List[int]] 
        :return: List[List[int]]
        """
        if not people: return []

        # 这里是一个算法，key降序排列，当key相同时按照value升序排列
        people = sorted(people, key=lambda x: (-x[0], x[1]))

        res = []
        for p in people:
            res.insert(p[1], p)
        return res
```

Scala

```
def reconstructQueue(people: Array[Array[Int]]): Array[Array[Int]] = {
    if (people == null) return null
    val person = people.sortBy(x => (-x(0), x(1)))

    for (elem <- person) {
      arr.insert(elem(1), elem)
    }
    arr.toArray
}
```

Java

```
思路：这题给了我们一个队列，队列中每个元素是一个pair，分别为身高和这个人前面身高不低于他的人数，让我们重组队列，使得每个pair的第二个参数都满足题意。
 *      1. 涉及到两个数或者区间的都先尝试按照对数组进行排序，我们先简单的按照h从大到小来进行排序
 *      2. 之所以需要从大到小，是因为在遍历时，我们可以随意的把当前元素往前移动（[7,0],[6,1],[7,1]）。它的前面都是比它大的，这样移动之后不会对前面的元素造成影响
 *      3. 反应到代码上就是先把元素记录下来，并从原数组中删除，再插入到指定位置
 *      4. 这里有个问题，对于h相同的元素，例如[5,2],[5,3]
 
public int[][] reconstructQueue(int[][] people) {

        if (people == null) return null;
        List<int[]> list = new LinkedList<>();

        Arrays.sort(people, (o1, o2) -> o1[0] == o2[0] ? o1[1] - o2[1] : o2[0] - o1[0]);
        for (int[] p: people) {
            list.add(p[1], p);
        }

        return list.toArray(people);
}
```



