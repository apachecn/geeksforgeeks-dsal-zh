# Python heapq 查找 2D 数组中的第 K 个最小元素

> 原文:[https://www . geesforgeks . org/python-heapq-find-kth-minist-element-2d-array/](https://www.geeksforgeeks.org/python-heapq-find-kth-smallest-element-2d-array/)

给定一个 n×n 矩阵和整数 k，找出给定 2D 数组中的第 k 个最小元素。

示例:

```
Input : mat = [[10, 25, 20, 40],
               [15, 45, 35, 30],
               [24, 29, 37, 48],
               [32, 33, 39, 50]]
        k =  7 
Output : 7th smallest element is 30

```

我们将使用类似的方法来解决这个问题，如[未排序数组中的第 K 个最小/最大元素](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)。

1.  使用 python 中的[堆](https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/)创建一个空的最小堆。
2.  现在分配结果变量中的第一行(列表)，并使用 **heapify** 方法将结果列表转换为最小堆。
3.  现在遍历剩余的行元素，并将它们推入创建的最小堆。
4.  现在使用 heapq 模块的 **nsmallest(k，iterable)** 方法得到 k 的最小元素。

```
# Function to find K'th smallest element in 
# a 2D array in Python
import heapq

def kthSmallest(input):

    # assign first row to result variable
    # and convert it into min heap
    result = input[0] 
    heapq.heapify(result)

    # now traverse remaining rows and push
    # elements in min heap
    for row in input[1:]:
         for ele in row:
              heapq.heappush(result,ele)

    # get list of first k smallest element because
    # nsmallest(k,list) method returns first k 
    # smallest element now print last element of 
    # that list
    kSmallest = heapq.nsmallest(k,result)
    print (k,"th smallest element is ",kSmallest[-1])

# Driver program
if __name__ == "__main__":
    input = [[10, 25, 20, 40],
           [15, 45, 35, 30],
           [24, 29, 37, 48],
           [32, 33, 39, 50]]
    k = 7
    kthSmallest(input)
```

输出:

```
7th smallest element is 30

```