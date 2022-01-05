# 根据数组出现次数的总和对数组进行降序排序

> 原文:[https://www . geeksforgeeks . org/基于出现次数总和的降序排序数组/](https://www.geeksforgeeks.org/sort-an-array-in-descending-order-based-on-the-sum-of-its-occurrence/)

给定一个可能包含重复元素的未排序整数数组，按照元素出现的降序对元素进行排序。如果存在一个以上的元素，它们的出现次数总和是相同的，那么，较大的一个将首先出现。
**例:**

> **输入:** arr[] = [2，4，1，2，4，2，10]
> **输出:** arr[] = [10，4，4，2，2，2，1]
> **说明:**
> 这里，2 出现 3 次，4 出现 2 次，1 出现 1 次，10 出现 1 次。
> 因此，
> 给定数组中 2 的所有出现的总和= 2 * 3 = 6，
> 4 的所有出现的总和= 4 * 2 = 8，
> 10 的所有出现的总和= 10 * 1 = 10，
> 1 的所有出现的总和= 1 * 1 = 1。
> 因此根据以上总和按降序对数组进行排序= [ 10，4，4，2，2，2，1 ]
> **输入 2:** arr[] = [2，3，2，3，2，1，1，9，6，9，1，2]
> **输出 2:**【9，9，2，2，2，6，3，3，1，1】

**进场:**

1.  创建一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，将元素映射到它的外观，即如果 a 出现一次，那么 a 将映射到 a，但是如果 a 出现 m 次，那么 a 将映射到 a*m。
2.  完成映射后，根据字典的值而不是关键字，按降序对字典进行排序。在平局的情况下，根据数值排序。
3.  最后，将排序后的字典关键字复制到最终的输出数组中，并根据它们的键值对获得频率，也就是说，如果 a 被映射到 a*m，这意味着我们需要在输出数组中包含 a，m 次。

以下是上述方法的实现:

## 计算机编程语言

```
# Python3 program to sort elements of
# arr[] in descending order of sum
# of its occurrence

def sort_desc(arr):

    # to store sum of all
    # occurrences of an elements
    d_sum = {}

    # to store count of
    # occurrence of elements
    d_count ={}

    # to store final result
    ans = []

    # to store maximum sum of occurrence
    mx = 0

    # Traverse and calculate sum
    # of occurrence and count of
    # occurrence of elements of arr[]
    for x in arr:
        if x not in d_sum:
            d_sum[x] = x
            d_count[x] = 1
        else:
            d_sum[x] += x
            d_count[x] += 1

    # sort d_sum in decreasing order of its value
    l = sorted(d_sum.items(), 
               reverse = True,
               key = lambda x:(x[1], x[0]))

    # store the final result
    for x in l:
        ans += [x[0]] * d_count[x[0]]

    return ans

# Driver Code
arr = [3, 5, 2, 2, 3, 1, 3, 1]
print(sort_desc(arr))
```

**Output:** 

```
[3, 3, 3, 5, 2, 2, 1, 1]
```

***时间复杂度:** O(N*log N)。*
***空间复杂度:** O(N)。*