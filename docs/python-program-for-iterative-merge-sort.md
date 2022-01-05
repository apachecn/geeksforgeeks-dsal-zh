# 迭代合并排序的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-iterative-merge-sort/](https://www.geeksforgeeks.org/python-program-for-iterative-merge-sort/)

以下是[合并排序](http://geeksquiz.com/merge-sort/)的典型递归实现，它使用最后一个元素作为轴心。

## 计算机编程语言

```
# Recursive Python Program for merge sort

def merge(left, right):
    if not len(left) or not len(right):
        return left or right

    result = []
    i, j = 0, 0
    while (len(result) < len(left) + len(right)):
        if left[i] < right[j]:
            result.append(left[i])
            i+= 1
        else:
            result.append(right[j])
            j+= 1
        if i == len(left) or j == len(right):
            result.extend(left[i:] or right[j:])
            break 

    return result

def mergesort(list):
    if len(list) < 2:
        return list

    middle = len(list)/2
    left = mergesort(list[:middle])
    right = mergesort(list[middle:])

    return merge(left, right)

seq = [12, 11, 13, 5, 6, 7]
print("Given array is")
print(seq); 
print("\n")
print("Sorted array is")
print(mergesort(seq))

# Code Contributed by Mohit Gupta_OMG 
```

更多详情请参考[迭代合并排序](https://www.geeksforgeeks.org/iterative-merge-sort/)整篇文章！