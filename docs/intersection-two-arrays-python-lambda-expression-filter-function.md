# Python 中两个数组的交集(Lambda 表达式和过滤函数)

> 原文:[https://www . geesforgeks . org/intersection-two-array-python-lambda-expression-filter-function/](https://www.geeksforgeeks.org/intersection-two-arrays-python-lambda-expression-filter-function/)

给定两个数组，找到它们的交集。

示例:

```
Input:  arr1[] = [1, 3, 4, 5, 7]
        arr2[] = [2, 3, 5, 6]
Output: Intersection : [3, 5]

```

这个问题我们已经有了解决方案，请参考[两个数组的交集](https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/)链接。我们将在 python 中使用 [Lambda 表达式](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/)和 [filter()](https://www.geeksforgeeks.org/lambda-filter-python-examples/) 函数快速解决这个问题。

```
# Function to find intersection of two arrays

def interSection(arr1,arr2):

     # filter(lambda x: x in arr1, arr2)  -->
     # filter element x from list arr2 where x
     # also lies in arr1
     result = list(filter(lambda x: x in arr1, arr2)) 
     print ("Intersection : ",result)

# Driver program
if __name__ == "__main__":
    arr1 = [1, 3, 4, 5, 7]
    arr2 = [2, 3, 5, 6]
    interSection(arr1,arr2)
```

输出:

```
Intersection : [3, 5]

```