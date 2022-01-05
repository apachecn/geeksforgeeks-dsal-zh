# Python 设置差异从重复数组中查找丢失的元素

> 原文:[https://www . geesforgeks . org/python-set-difference-find-lost-element-replicated-array/](https://www.geeksforgeeks.org/python-set-difference-find-lost-element-duplicated-array/)

给定两个数组，除了一个元素之外，其余都是重复的，也就是说，其中一个数组的一个元素丢失了，我们需要找到那个丢失的元素。

示例:

```
Input:  A = [1, 4, 5, 7, 9]
        B = [4, 5, 7, 9]
Output: [1]
1 is missing from second array.

Input: A = [2, 3, 4, 5
       B = 2, 3, 4, 5, 6]
Output: [6]
6 is missing from first array.

```

这个问题我们已经有了解决方案，请参考[从重复的数组中找到丢失的元素](https://www.geeksforgeeks.org/find-lost-element-from-a-duplicated-array/)。我们可以使用[设置差分逻辑](https://www.geeksforgeeks.org/sets-in-python/)在 python 中快速解决这个问题。方法很简单，只需在**中转换两个列表，设置**并执行 **A-B** 操作，其中 len(A) > len(B)。

```
# Function to find lost element from a duplicate
# array

def lostElement(A,B):

     # convert lists into set
     A = set(A)
     B = set(B)

     # take difference of greater set with smaller
     if len(A) > len(B):
         print (list(A-B))
     else:
         print (list(B-A))

# Driver program
if __name__ == "__main__":
    A = [1, 4, 5, 7, 9]
    B = [4, 5, 7, 9]
    lostElement(A,B)
```

输出:

```
[1]

```