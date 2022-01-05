# Python 程序查找给定差的一对

> 原文:[https://www . geesforgeks . org/python-program-to-find-a-pair-with-then-difference/](https://www.geeksforgeeks.org/python-program-to-find-a-pair-with-the-given-difference/)

给定一个未排序的数组和一个数字 n，找出数组中是否有一对元素的差为 n。
**示例:**

```
Input: arr[] = {5, 20, 3, 2, 50, 80}, n = 78
Output: Pair Found: (2, 80)

Input: arr[] = {90, 70, 20, 80, 50}, n = 45
Output: No Such Pair
```

最简单的方法是运行两个循环，外部循环挑选第一个元素(较小的元素)，内部循环寻找由外部循环加上 n 挑选的元素。这个方法的时间复杂度是 O(n^2).
我们可以使用排序和二分搜索法来提高时间复杂度到 O(nLogn)。第一步是按升序对数组进行排序。一旦数组被排序，从左到右遍历数组，对于每个元素 arr[i]，arr[I+1]中 arr[i] + n 的二分搜索法..n-1]。如果找到该元素，则返回该对。
第一步和第二步都采用 0(nLogn)。所以整体复杂度是 O(nLogn)。
上述算法的第二步可以改进为 O(n)。第一步保持不变。第二步的想法是取两个索引变量 I 和 j，分别初始化为 0 和 1。现在运行一个线性循环。如果 arr[j]–arr[i]小于 n，我们需要寻找更大的 arr[j]，所以增量为 j .如果 arr[j]–arr[I]大于 n，我们需要寻找更大的 arr[I]，所以增量为 I .感谢 Aashish Barnwal 提出这种方法。
下面的代码只是针对算法的第二步，它假设数组已经排序了。

## 计算机编程语言

```
# Python program to find a pair with the given difference

# The function assumes that the array is sorted
def findPair(arr,n):

    size = len(arr)

    # Initialize positions of two elements
    i,j = 0,1

    # Search for a pair
    while i < size and j < size:

        if i != j and arr[j]-arr[i] == n:
            print "Pair found (",arr[i],",",arr[j],")"
            return True

        elif arr[j] - arr[i] < n:
            j+=1
        else:
            i+=1
    print "No pair found"
    return False

# Driver function to test above function
arr = [1, 8, 30, 40, 100]
n = 60
findPair(arr, n)

# This code is contributed by Devesh Agrawal
```

**输出:**

```
Pair Found: (40, 100)
```

哈希也可以用来解决这个问题。创建一个空哈希表 HT。遍历数组，使用数组元素作为哈希键，并在 HT 中输入它们。再次遍历数组，在 HT 中寻找值 n + arr[i]。

更多详情请参考[整篇文章找到一对给定差异的](https://www.geeksforgeeks.org/find-a-pair-with-the-given-difference/)！