# 二进制插入排序的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-binary-insert-sort/](https://www.geeksforgeeks.org/python-program-for-binary-insertion-sort/)

我们可以使用二分搜索法减少[正常插入排序](https://www.geeksforgeeks.org/insertion-sort/)中的比较次数。二进制插入排序查找使用二分搜索法查找在每次迭代中插入所选项目的正确位置。
在正常插入中，排序在最坏的情况下需要 O(i)(第一次迭代)。我们可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)将其减少到 0(logi)。

## 计算机编程语言

```
# Python Program implementation  
# of binary insertion sort

def binary_search(arr, val, start, end):
    # we need to distinugish whether we should insert
    # before or after the left boundary.
    # imagine [0] is the last step of the binary search
    # and we need to decide where to insert -1
    if start == end:
        if arr[start] > val:
            return start
        else:
            return start+1

    # this occurs if we are moving beyond left\'s boundary
    # meaning the left boundary is the least position to
    # find a number greater than val
    if start > end:
        return start

    mid = (start+end)/2
    if arr[mid] < val:
        return binary_search(arr, val, mid+1, end)
    elif arr[mid] > val:
        return binary_search(arr, val, start, mid-1)
    else:
        return mid

def insertion_sort(arr):
    for i in xrange(1, len(arr)):
        val = arr[i]
        j = binary_search(arr, val, 0, i-1)
        arr = arr[:j] + [val] + arr[j:i] + arr[i+1:]
    return arr

print("Sorted array:")
print insertion_sort([37, 23, 0, 17, 12, 72, 31,
                        46, 100, 88, 54])

# Code contributed by Mohit Gupta_OMG 
```

更多详情请参考[二进制插入排序](https://www.geeksforgeeks.org/binary-insertion-sort/)整篇文章！