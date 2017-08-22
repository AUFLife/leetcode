### 136. Single Number

Easy



Given an array of integers, every element appearstwiceexcept for one. Find that single one.

**Note:**  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Python:

```
# Method 1 use extra memory
return sum(list(set(num)) * 2 - sum(sums)

# Method 2 
return reduce(lamdba x,y: x ^ y, nums)
```

Scala:

```
val i = a.reduce((x, y) => x ^ y)
```

Java:

```
        int res = nums[0];
        for (int i = 0; i < nums.length; i++) {
            res = res ^ nums[i];
        }
        return res;
```



