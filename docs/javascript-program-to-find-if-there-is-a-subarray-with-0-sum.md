# Javascript 程序查找是否有 0 和的子数组

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-find-if-a-subarray-with-0-sum/](https://www.geeksforgeeks.org/javascript-program-to-find-if-there-is-a-subarray-with-0-sum/)

给定一个正数和负数的数组，找出是否有一个和为 0 的子数组(大小至少为 1)。

**示例:**

> **输入:** {4，2，-3，1，6}
> **输出:**真
> **说明:**
> 有一个从指标 1 到指标 3 的零和子阵。
> 
> **输入:** {4，2，0，1，6}
> **输出:**:真
> **说明:**
> 从指标 2 到 2 有一个零和的子阵。
> 
> **输入:** {-3，2，3，1，6}
> 输出:假

一个**简单的解决方案**就是逐个考虑所有子阵，检查每个子阵的和。我们可以运行两个循环:外部循环选择一个起点 I，内部循环尝试从 I 开始的所有子阵列(实现参见[本](https://www.geeksforgeeks.org/find-subarray-with-given-sum/))。该方法的时间复杂度为 O(n <sup>2</sup> )。
我们也可以**使用哈希**。其思想是迭代数组，对于每个元素 arr[i]，计算从 0 到 I 的元素之和(这可以简单地用 sum += arr[i]来完成)。如果之前已经看到过当前总和，那么就有一个零和数组。散列用于存储和值，以便我们可以快速存储总和，并找出当前总和之前是否被看到。
**示例:**

```
arr[] = {1, 4, -2, -2, 5, -4, 3}

If we consider all prefix sums, we can
notice that there is a subarray with 0
sum when :
1) Either a prefix sum repeats or
2) Or prefix sum becomes 0.

Prefix sums for above array are:
1, 5, 3, 1, 6, 2, 5

Since prefix sum 1 repeats, we have a subarray
with 0 sum. 
```

下面是上述方法的实现。

## java 描述语言

```
// A Javascript program to
//  find if there is a zero sum subarray

const subArrayExists = (arr) => {
    const sumSet = new Set();

    // Traverse through array 
    // and store prefix sums
    let sum = 0;
    for (let i = 0 ; i < arr.length ; i++)
    {
        sum += arr[i];

        // If prefix sum is 0 
        // or it is already present
        if (sum === 0 || sumSet.has(sum))
            return true;

        sumSet.add(sum);
    }
    return false;
}

// Driver code

const arr =  [-3, 2, 3, 1, 6];
if (subArrayExists(arr))
    console.log("Found a subarray with 0 sum");
else
    console.log("No Such Sub Array Exists!");
```

**Output**

```
No Such Sub Array Exists!
```

**这个解的时间复杂度**可以认为是 O(n)，假设我们有很好的哈希函数，允许在 O(1)时间内进行插入和检索操作。
**空间复杂性** : O(n)。这里我们需要额外的空间给无序集来插入数组元素。

更多详情请参考[整篇文章查找是否有求和为 0 的子阵](https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/)！