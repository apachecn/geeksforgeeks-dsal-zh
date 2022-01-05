# Python 程序在 O(n)时间和 O(1)额外空间内重新排列正负数

> 原文:[https://www . geesforgeks . org/python-program-to-重排-正负数-on-time-and-O1-extra-space/](https://www.geeksforgeeks.org/python-program-to-rearrange-positive-and-negative-numbers-in-on-time-and-o1-extra-space/)

数组包含随机顺序的正数和负数。重新排列数组元素，使正数和负数交替出现。正数和负数的数量不必相等。如果有更多的正数，它们会出现在数组的末尾。如果有更多的负数，它们也会出现在数组的末尾。
例如，如果输入数组是[-1，2，-3，4，5，6，-7，8，9]，那么输出应该是[9，-7，8，-3，5，-1，2，4，6]
**注:**划分过程改变元素的相对顺序。也就是说，用这种方法不能保持元素出现的顺序。[维护本问题中元素的出现顺序见本](https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/)。
解决方法是先用 QuickSort 的划分过程将正数和负数分开。在划分过程中，将 0 视为透视元素的值，以便所有负数都放在正数之前。一旦负数和正数被分开，我们从第一个负数和第一个正数开始，用下一个正数交换每个交替的负数。

## 计算机编程语言

```
#  Python program to put positive numbers at even indexes (0,  // 2, 4,..) and
#  negative numbers at odd indexes (1, 3, 5, ..)

# The main function that rearranges elements of given array. 
# It puts  positive elements at even indexes (0, 2, ..) and 
# negative numbers at odd indexes (1, 3, ..).
def rearrange(arr, n):
    # The following few lines are similar to partition process
    # of QuickSort.  The idea is to consider 0 as pivot and
    # divide the array around it.
    i = -1
    for j in range(n):
        if (arr[j] < 0):
            i += 1
            # swapping of arr
            arr[i], arr[j] = arr[j], arr[i]

    # Now all positive numbers are at end and negative numbers
    # at the beginning of array. Initialize indexes for starting
    # point of positive and negative numbers to be swapped
    pos, neg = i+1, 0

    # Increment the negative index by 2 and positive index by 1,
    # i.e., swap every alternate negative number with next 
    # positive number
    while (pos < n and neg < pos and arr[neg] < 0):

        # swapping of arr
        arr[neg], arr[pos] = arr[pos], arr[neg]
        pos += 1
        neg += 2

# A utility function to print an array
def printArray(arr, n):

    for i in range(n):
        print arr[i],

# Driver program to test above functions
arr = [-1, 2, -3, 4, 5, 6, -7, 8, 9]
n = len(arr)
rearrange(arr, n)
printArray(arr, n)

# Contributed by Afzal
```

**输出:**

```
    4   -3    5   -1    6   -7    2    8    9
```

**时间复杂度:** O(n)，其中 n 为给定数组中的元素个数。
**辅助空间:** O(1)

更多详情请参考[整篇文章在 O(n)时间和 O(1)额外空间](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers-publish/)重新排列正负数！