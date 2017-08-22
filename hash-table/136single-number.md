### 136. Single Number 

Difficulty : **Easy**



Given an array of integers, every element appearstwiceexcept for one. Find that single one.

**Note:**  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Soultion:**

Python

```py
# Method 1 user extra memory
return sum(list(set(nums))) * 2 - sum(nums)

# Method 2
return reduce(lambda x,y: x ^ y, nums)
```

Scala

```Scala
val res = a.reduce((x, y) => x ^ y)
```

Java

```java
int res = nums[0];
for (int i = 0; i < nums.length; i++) {
    res = res ^ nums[i];
}
return res;
```



