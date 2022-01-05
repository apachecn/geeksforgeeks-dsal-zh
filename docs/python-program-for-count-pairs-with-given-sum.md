# 给定和的计数对的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-计数对给定总和的程序/](https://www.geeksforgeeks.org/python-program-for-count-pairs-with-given-sum/)

给定一个整数数组和一个数“和”，求数组中和等于“和”的整数对的个数。

**示例:**

```
Input  :  arr[] = {1, 5, 7, -1}, 
          sum = 6
Output :  2
Pairs with sum 6 are (1, 5) and (7, -1)

Input  :  arr[] = {1, 5, 7, -1, 5}, 
          sum = 6
Output :  3
Pairs with sum 6 are (1, 5), (7, -1) &
                     (1, 5)         

Input  :  arr[] = {1, 1, 1, 1}, 
          sum = 2
Output :  6
There are 3! pairs with sum 2.

Input  :  arr[] = {10, 12, 10, 15, -1, 7, 6, 
                   5, 4, 2, 1, 1, 1}, 
          sum = 11
Output :  9
```

预期时间复杂度 O(n)

**天真的解决方案–**一个**简单的解决方案**是遍历每个元素，检查数组中是否有另一个数字可以添加到其中以给出总和。

## 蟒蛇 3

```
# Python3 implementation of simple method
# to find count of pairs with given sum.

# Returns number of pairs in arr[0..n-1]
# with sum equal to 'sum'

def getPairsCount(arr, n, sum):

    count = 0  # Initialize result

    # Consider all possible pairs
    # and check their sums
    for i in range(0, n):
        for j in range(i + 1, n):
            if arr[i] + arr[j] == sum:
                count += 1

    return count

# Driver function
arr = [1, 5, 7, -1, 5]
n = len(arr)
sum = 6
print("Count of pairs is",
      getPairsCount(arr, n, sum))

# This code is contributed by Smitha Dinesh Semwal
```

**Output**

```
Count of pairs is 3
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)

**高效解决方案–**
在 O(n)时间内可能会有更好的解决方案。以下是算法–

1.  创建一个映射来存储数组中每个数字的频率。(需要单次遍历)
2.  在下一次遍历中，对于每个元素，检查它是否可以与任何其他元素(除了它本身！)来给出期望的总和。相应地增加计数器。
3.  在完成第二次遍历后，我们会在计数器中存储两倍的所需值，因为每对都被计数两次。因此将计数除以 2 并返回。

以下是上述思路的实现:

## 蟒蛇 3

```
# Python 3 implementation of simple method
# to find count of pairs with given sum.
import sys

# Returns number of pairs in arr[0..n-1]
# with sum equal to 'sum'

def getPairsCount(arr, n, sum):

    m = [0] * 1000

    # Store counts of all elements in map m
    for i in range(0, n):
        m[arr[i]] += 1

    twice_count = 0

    # Iterate through each element and increment
    # the count (Notice that every pair is
    # counted twice)
    for i in range(0, n):

        twice_count += m[sum - arr[i]]

        # if (arr[i], arr[i]) pair satisfies the
        # condition, then we need to ensure that
        # the count is  decreased by one such
        # that the (arr[i], arr[i]) pair is not
        # considered
        if (sum - arr[i] == arr[i]):
            twice_count -= 1

    # return the half of twice_count
    return int(twice_count / 2)

# Driver function
arr = [1, 5, 7, -1, 5]
n = len(arr)
sum = 6

print("Count of pairs is", getPairsCount(arr,
                                         n, sum))

# This code is contributed by
# Smitha Dinesh Semwal
```

**Output**

```
Count of pairs is 3
```

更多详情请参考[给定和](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)计数对的完整文章！