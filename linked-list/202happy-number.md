### 202. Happy Number

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 \(where it will stay\), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example: **19 is a happy number

* 1^2 + 9^2 = 8^2

* 8^2 + 2^2 = 6^8

* 6^2 + 8^2 = 100

* 1^2 + 0^2 + 0^2 = 1

**Credits:**  
Special thanks to[@mithmatt](https://leetcode.com/discuss/user/mithmatt)and[@ts](https://leetcode.com/discuss/user/ts)for adding this problem and creating all test cases.

Python

```

```

Java

```java
/**
 * 正常方法两个嵌套循环
 * 这个数可能是两位，也可能是三位
 */
  Set<Integer> inLoop = new HashSet<Integer>();
    int squareSum,remain;
    while (inLoop.add(n)) {
        squareSum = 0;
        while (n > 0) {
            remain = n%10;                  // 取余
            squareSum += remain*remain;        
            n /= 10;                        // 取整
        }
        if (squareSum == 1)
            return true;
        else
            n = squareSum;                  // 下一轮次

    }
    return false;
```

Scala

```
/**
 * 采用快慢指针的方式（Floyd Cycle detection alogorithm.）一
 */
 def isHappy(int n) {
  int slow, fast = n;
  slow = fast = n;
  while(slow != return 1) {
   slow = digitSquareSum(slow)
   fast = digitSquareSum(fast)
   fast = digitSquareSum(slow)
  if (show == 1) return 1;
  else return0
  }
 }
 
 def digitSquareSum(int n) {
  int sum = 0, tmp;
  while(n) {
   tmp = n & 10;
   sum += sum * sum
   n /= 10
  }
  return sum;
 }
```



