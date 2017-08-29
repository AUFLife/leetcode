### 448. Find All Numbers Disappeared in an Array

Difficulty : Easy

Given an array of integers where 1 ≤ a\[i\] ≤n\(n= size of array\), some elements appear twice and others appear once.

Find all the elements of \[1,n\] inclusive that do not appear in this array.

Could you do it without extra space and in O\(n\) runtime? You may assume the returned list does not count as extra space.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

**Solution:**

```
/**
* 由于题目中所有数字都大于等于1且小于等于n，而n为数组长度这一条件。所以可以用数组下标作为
* 索引标记哪些数字出现过，标记法为将出现数字对应下标的数字标为负数
*
* 1. 计算出数组中出现的数字x的下标形式，则下标index = |x| - 1，可将数组a中得a[index]标记为负数来标记数字x出现在数组中
* 2. 若数组中某数字已为负数，说明该数字在数组中出现过
* 4. 最终遍历数组，若a[i]为正数，表明数字i + 1在数组中没有出现过
*
* Time Complexity: O(n)
* Space Complexity: O(n)
* @param nums
* @return
*/
```



时间复杂度: O\(n\)

空间复杂度: O\(n\)

Python

```py
def findDisappearedNumbers(nums):
    """ 
    For each number i in nums,
    we mark the bumber that i points as negative.
    Then we filter the list, get all the indexes
    who points to a positive number
    :param nums: List[int] 
    :return: List[int]
    """
    for i in xrange(len(nums)):
        # create index
        index = abs(nums[i]) - 1
        nums[index] = -abs(nums[index])

    return [i + 1 for i in xrange(len(nums)) if nums[i] > 0]
```

Scala

```
/**
    * 因为数组长度为n，且数组范围在[1,n]之间，因此可以根据数组下标作为索引来标记哪些数字出现过，标记方法为将出现数字对应下表的数字标为负数
    * 1. 计算出数组中出现的数字x的下标形式，则下标形式为index = |x| - 1, 可将数组a[index]标为负数来标记数字x出现在数组中
    * 2. 若数组中某数字已经为负数，说明该数字已出现过
    * 3. 最后进行一次遍历，数组中某数字a[i]为正，表明i + 1在数组中没有出现过
    * @param nums
    * @return
    */
  def findDisappearedNumbers(nums: Array[Int]): List[Integer] = {
    val res = new ArrayBuffer[Integer]()
    if (nums.isEmpty) { return res.toList}
    for (i <- nums.indices) {
      val index = Math.abs(nums(i)) - 1
      nums(index) = if (nums(index) > 0) -nums(index) else nums(index)
    }
    for (i <- nums.indices) {
      if (nums(i) > 0) {
        res += (i + 1)
      }
    }
    res.toList
  }
```

Java

```
private List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> ret = new ArrayList<>();
        if (nums == null) {
            return ret;
        }
        // [4, 3, 2, 7, 8, 2, 3, 1]
        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            // 第一列数组下标，指定的数字作为索引，根据这个作为索引，可以遍历到数组所有的值，将该索引标明的位置置为-1，表明该位置表示数字出现过。再次遍历数组，大约0的数字所属位置则为未曾出现的数字，加入结果中
            // i    nums[i]
            // 出现数字（nums[i]），下标即为当前数字前一数字
            // i=0, nums[i]=4, index=3, nums[index] > 0 -> -7
            // i=1, nums[i]=3, index=2, nums[index] > 0 -> -2
            // i=2, nums[i]=2, index=1, nums[index] > 0 -> -3
            // i=3, nums[i]=7, index=6, nums[index] > 0 -> -3
            // i=4, nums[i]=8, index=7, nums[index] > 0 -> -1
            // i=5, nums[i]=2, index=1, nums[index] > 0 -> -3
            // i=6, nums[i]=3, index=2, nums[index] > 0 -> -2
            // i=7, nums[i]=1, index=0, nums[index] > 0 -> -4
            nums[index] = nums[index] > 0 ? -nums[index] : nums[index];
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                ret.add(i + 1);
            }
        }
        return ret;
    }
```



