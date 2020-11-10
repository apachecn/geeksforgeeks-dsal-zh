# 打印最接近数组中第`K`个最小元素的`X`个数组元素

> 原文：[https://www.geeksforgeeks.org/print-x-array-elements-closest-to-the-kth-smallest-element-in-the-array/](https://www.geeksforgeeks.org/print-x-array-elements-closest-to-the-kth-smallest-element-in-the-array/)



给定两个整数`K`， `X`和一个[数组](https://www.geeksforgeeks.org/array-data-structure/)`arr[]`，它们由`N`个不同的元素组成， 任务是从给定数组中找到最接近[第`K`个最小元素](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)的`X`个元素。

**示例**：

> **输入**：`arr[] = {1, 2, 3, 4, 10}, K = 3, X = 2`
> **输出**：`2 3`
> **说明**：给定数组中存在的第`K`个最小元素是 3，最接近`X = 2`的数组元素是`{2, 3}`或`{3, 4}`。
> 因此，所需的输出为`2 3`。
> 
> **输入**：`arr[] = {1, 9, 8, 2, 7, 3, 6, 4, 5, 10, 13, 12, 16, 14, 11, 15}, K = 3,  X = 5`
> **输出**：`1 2 3 4 5`

**朴素的方法**：解决此问题的最简单方法是[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)排序，并使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)，打印最接近给定数组的第`K`个最小元素的`X`。

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(1)`

**有效方法**：为了优化上述方法，其思想是使用[中值来有效计算给定数组的 **K <sup>th</sup>** 最小元素的值 选择算法](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)。 请按照以下步骤解决问题：

*   使用[中值选择算法](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)计算给定数组的第`K`小，即`KthElem`。

*   初始化一个数组，例如说`diff[]`，以存储`arr[i]`和`KthElem`的绝对差。

*   创建一个[映射](https://www.geeksforgeeks.org/defaultdict-in-python/)，例如说**映射**以将数组的每个元素映射到当前元素和`KthElem`的绝对差。

*   遍历给定数组，并将`arr[i]`附加到`map[abs(KthElem – arr[i])]`。

*   使用[中值选择算法](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)计算`diff[]`数组的第`X`个最小元素，例如`XthElem`，来打印`X`个最接近的项目。

*   最后，遍历`diff[]`数组，并检查`XthElem`是否小于或等于`diff[i]`。 如果确定为`true`，则在**映射**的帮助下打印数组的元素。

下面是上述方法的实现：

## Python3

```py

# Python3 program to implement 
# the above approach 

import collections 

# Function to swap 
# two elements of array 
def swap(arr, a, b): 
    temp = arr[a] 
    arr[a] = arr[b] 
    arr[b] = temp 

# Function to partition  
# the array around x 
def partition(arr, l, r, x): 

    # Traverse array  
    # from index l to r 
    for i in range(l, r): 

        # partition array 
        # around x 
        if arr[i] == x: 
            swap(arr, r, i) 
            break

    x = arr[r] 
    i = l 

    # Traverse array  
    # from index l to r  
    for j in range(l, r): 
        if (arr[j] <= x): 
            swap(arr, i, j) 
            i += 1
    swap(arr, i, r) 
    return i 

# Function to find 
# median of arr[]  
# from index l to l + n 
def findMedian(arr, l, n): 
    lis = [] 
    for i in range(l, l + n): 
        lis.append(arr[i]) 

    # Sort the array 
    lis.sort() 

    # Return middle element 
    return lis[n // 2] 

# Function to get  
# the kth smallest element 
def kthSmallest(arr, l, r, k): 

    # If k is smaller than 
    # number of elements 
    # in array 
    if (k > 0 and 
        k <= r - l + 1): 

        # Stores count of  
        # elements in arr[l..r] 
        n = r - l + 1

        # Divide arr[] in groups 
        # of size 5, calculate  
        # median  of every group 
        # and store it in 
        # median[] array. 
        median = [] 

        i = 0
        while (i < n // 5): 
            median.append( 
            findMedian(arr,  
                l + i * 5, 5)) 
            i += 1

        # For last group with 
        # less than 5 elements 
        if (i * 5 < n): 
            median.append( 
             findMedian(arr,  
                l + i * 5, n % 5)) 
            i += 1

        # If median[] has  
        # only one element 
        if i == 1: 
            medOfMed = median[i - 1] 

        # Find median of all medians 
        # using recursive call. 
        else: 
            medOfMed = kthSmallest( 
             median, 0, i - 1, i // 2) 

        # Stores position of pivot 
        # element in sorted array 
        pos = partition(arr, l, r, 
                         medOfMed) 

        # If position is same as k 
        if (pos - l == k - 1): 
            return arr[pos] 

        # If position is more,     
        if (pos - l > k - 1):  

            # recur for left subarray 
            return kthSmallest(arr, l,  
                          pos - 1, k) 

        # Else recur for right subarray 
        return kthSmallest(arr, pos + 1,  
                    r, k - pos + l - 1) 

    # If k is more than  
    # number of elements 
    # in the array 
    return 999999999999

# Function to print  
def closestElements(arr, k, x): 

    # Stores size of arr 
    n = len(arr) 

    # Stores kth smallest  
    # of the given array 
    KthElem = kthSmallest( 
            arr, 0, n - 1, k) 

    # Store the value of  
    # abs(KthElem - arr[i])  
    diff = [] 

    # Create a map to map  
    # array element to 
    # abs(KthElem - arr[i]) 
    maps = collections.defaultdict( 
                              list) 
    for elem in arr: 

        # Stres the value of  
        # abs(elem - KthElem) 
        temp = abs(elem - KthElem) 

        # map array elements 
        maps[temp].append(elem) 

        # append temp 
        diff.append(temp) 

    XthElem = kthSmallest(diff, 0,  
                        n - 1, x) 

    # Store X closest elements 
    res = set() 

    # Traverse diff[] array 
    for dx in diff: 

        # If absolute difference is  
        # less than or eqaul to XthElem 
        if dx <= XthElem: 

            # Append closest elements  
            for elem in maps[dx]: 
                if len(res) < x: 
                  res.add(elem) 
    return res 

# Driver Code 
if __name__ == '__main__': 

    arr = [1, 2, 3, 4, 10, 15] 
    k = 3
    x = 2

    # Store X closest elements 
    res = closestElements(arr, k, x) 

    # Print X closest elements 
    for i in res: 
        print(i, end =" "); 

```

**输出**：

```
2 3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



