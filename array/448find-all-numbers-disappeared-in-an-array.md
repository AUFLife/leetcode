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

```

Java

```

```



