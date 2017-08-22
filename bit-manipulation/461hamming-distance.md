### 461. Hamming Distance

Difficulty : **Easy**



The[Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance)between two integers is the number of positions at which the corresponding bits are different.

Given two integers`x`and`y`, calculate the Hamming distance.

**Note:**  
0 ≤`x`,`y`&lt; 231.

**Example:**

```java
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ?   ?

The above arrows point to positions where the corresponding bits are different.
```

**Solution:**

Python

```

```

Scala

```Scala
/**
    * 直接解法：在循环中依次判断x和y的对应位是否相同, 可以通过异或来解决
    * 异或性质xor：相同为0，不同为1
    * 与and：bit位同时为1则为1，否则为0
    * 那么怎样确定异或结果中1的个数呢？
    * 可以通过 xorValue & (xorValue - 1), xorValue的最低位1都会变成0，即每次去掉一个1，直到其值为0
    * 举例：
    *   00110 & 00101 = 00100
    *   00100 & 00011 = 00000
    *
    * @param x
    * @param y
    */
  def hammingDistance(x: Int, y: Int) = {
    var xorValue = x ^ y
    var count = 0
    while (xorValue > 0) {
      xorValue &= xorValue - 1
      count += 1
    }
    count
  }
```

Java

```java
   public int hammingDistance(int x, int y) {
       int xorValue = x ^ y;
        int dist = 0;

        //计算1的个数
        while(xorValue) {
           xorValue = xorValue & (xorValue - 1);
           ++ dist;
        }

        return dist; 
    }
```



