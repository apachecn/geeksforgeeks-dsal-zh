# Python3 从重复数组中查找丢失元素的程序

> 原文:[https://www . geesforgeks . org/python 3-从重复数组中寻找丢失元素的程序/](https://www.geeksforgeeks.org/python3-program-to-find-lost-element-from-a-duplicated-array/)

假设两个数组除了一个元素之外都是重复的，也就是说其中一个数组的一个元素丢失了，我们需要找到那个丢失的元素。
**例:**

```
Input:  arr1[] = {1, 4, 5, 7, 9}
        arr2[] = {4, 5, 7, 9}
Output: 1
1 is missing from second array.

Input: arr1[] = {2, 3, 4, 5}
       arr2[] = {2, 3, 4, 5, 6}
Output: 6
6 is missing from first array.
```

一个**简单的解决方案**是迭代数组，逐元素检查，当发现不匹配的元素时标记缺失的元素，但是这个解决方案需要数组的线性时间过大。
另一个**高效解决方案**是基于 [](http://geeksquiz.com/binary-search/) 一个[二分搜索法](http://geeksquiz.com/binary-search/)的方法。算法步骤如下:

1.  在更大的阵列中启动二分搜索法，获得中间 as (lo + hi) / 2
2.  如果两个数组的值相同，那么缺少的元素必须在右边，因此将 lo 设置为 mid
3.  否则将 hi 设置为 mid，因为如果 mid 元素不相等，丢失的元素必须在更大数组的左边。
4.  一种特殊情况是单独处理的，对于单元素和零元素数组，单元素本身将是缺失的元素。
    如果第一个元素本身不相等，那么该元素将是缺失的元素。/li >

以下是上述步骤的实施

## 蟒蛇 3

```
# Python3 program to find missing
# element from same arrays 
# (except one missing element)

# Function to find missing element based
# on binary search approach. arr1[] is 
# of larger size and N is size of it. 
# arr1[] and arr2[] are assumed
# to be in same order.
def findMissingUtil(arr1, arr2, N):

    # special case, for only element 
    # which is missing in second array
    if N == 1:
        return arr1[0];

    # special case, for first
    # element missing
    if arr1[0] != arr2[0]:
        return arr1[0]

    # Initialize current corner points
    lo = 0
    hi = N - 1

    # loop until lo < hi
    while (lo < hi):

        mid = (lo + hi) / 2

        # If element at mid indices
        # are equal then go to 
        # right subarray
        if arr1[mid] == arr2[mid]:
            lo = mid
        else:
            hi = mid

        # if lo, hi becomes 
        # contiguous, break
        if lo == hi - 1:
            break

    # missing element will be at
    # hi index of bigger array
    return arr1[hi]

# This function mainly does basic
# error checking and calls 
# findMissingUtil
def findMissing(arr1, arr2, M, N):

    if N == M-1:
        print("Missing Element is",
            findMissingUtil(arr1, arr2, M))
    elif M == N-1:
        print("Missing Element is",
            findMissingUtil(arr2, arr1, N))
    else:
        print("Invalid Input")

# Driver Code
arr1 = [1, 4, 5, 7, 9]
arr2 = [4, 5, 7, 9]
M = len(arr1)
N = len(arr2)
findMissing(arr1, arr2, M, N)

# This code is contributed by Smitha Dinesh Semwal
```

输出:

```
Missing Element is 1
```

**如果输入数组不在** **中，该怎么办？**
在这种情况下，缺失的元素只是两个数组所有元素的异或。感谢 Yolo Song 的建议。

## 蟒蛇 3

```
# Python 3 program to find
# missing element from one array
# such that it has all elements
# of other array except
# one. Elements in two arrays
# can be in any order.

# This function mainly does XOR of all elements
# of arr1[] and arr2[]
def findMissing(arr1,arr2, M, N):
    if (M != N-1 and N != M-1):

        print("Invalid Input")
        return

    # Do XOR of all element
    res = 0
    for i in range(0,M):
        res = res^arr1[i];
    for i in range(0,N):
        res = res^arr2[i]

    print("Missing element is",res)

# Driver Code
arr1 = [4, 1, 5, 9, 7]
arr2 = [7, 5, 9, 4]
M = len(arr1) 
N = len(arr2)
findMissing(arr1, arr2, M, N)

# This code is contributed
# by Smitha Dinesh Semwal
```

**输出:**

```
Missing Element is 1
```

更多详细信息，请参考完整文章[从重复数组](https://www.geeksforgeeks.org/find-lost-element-from-a-duplicated-array/)中查找丢失元素！