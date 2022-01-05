# Python 列表理解从两个数组中找到给定和的对

> 原文:[https://www . geesforgeks . org/python-list-intensity-find-pair-given-sum-two-arrays/](https://www.geeksforgeeks.org/python-list-comprehension-find-pair-given-sum-two-arrays/)

给定两个不同元素的未排序数组，任务是从两个数组中找出和等于 x 的所有对。

示例:

```
Input :  arr1 = [-1, -2, 4, -6, 5, 7]
         arr2 = [6, 3, 4, 0]  
         x = 8
Output : [(5, 3), (4, 4)]

Input : arr1 = [1, 2, 4, 5, 7] 
        arr2 = [5, 6, 3, 4, 8]  
        x = 9
Output : [(1, 8), (4, 5), (5, 4)]

```

这个问题我们已经有了解决方案，请参考[给定两个未排序的数组，找到所有和为 x 的对](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)链接。我们可以使用[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)在 python 中快速解决这个问题。方法很简单，我们将考虑所有那些对，对于这些对**如果 k 位于 arr2** 中，那么 **x-k 应该位于 arr1** 中，所以对将是(x-k，k)。

```
# Function to find all pairs whose sum is x in 
# two arrays

def allPairs(arr1,arr2,x):

     # finds all pairs in two arrays
     # whose sum is x
     print ([(x-k,k) for k in arr2 if (x-k) in arr1])

# Driver program
if __name__ == "__main__":
    arr1 = [-1, -2, 4, -6, 5, 7]
    arr2 = [6, 3, 4, 0]  
    x = 8
    allPairs(arr1,arr2,x)
```

**复杂度:** O(n*n)
输出:

```
[(5, 3), (4, 4)]

```