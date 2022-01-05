# 数组平衡索引的 Python3 程序

> 原文:[https://www . geeksforgeeks . org/python 3-数组平衡索引程序/](https://www.geeksforgeeks.org/python3-program-for-equilibrium-index-of-an-array/)

数组的平衡索引是这样一种索引，即较低索引处的元素之和等于较高索引处的元素之和。例如，在数组 A 中:

**示例:**

> **输入** : A[] = {-7，1，5，2，-4，3，0}
> 输出 : 3
> 3 是均衡指标，因为:
> A[0]+A[1]+A[2]= A[4]+A[5]+A[6]
> 
> **输入** : A[] = {1，2，3}
> **输出** : -1

写一个函数*int balance(int[]arr，int n)*；给定大小为 n 的序列 arr[,返回一个平衡指数(如果有的话),如果不存在平衡指数，则返回-1。

**方法 1(简单但低效)**
使用两个循环。外循环遍历所有元素，内循环找出外循环选择的当前索引是否为平衡索引。这个解决方案的时间复杂度是 O(n^2).

## 蟒蛇 3

```
# Python program to find equilibrium 
# index of an array

# function to find the equilibrium index
def equilibrium(arr):
    leftsum = 0
    rightsum = 0
    n = len(arr)

    # Check for indexes one by one 
    # until an equilibrium index is found
    for i in range(n):
        leftsum = 0
        rightsum = 0

        # get left sum
        for j in range(i):
            leftsum += arr[j]

        # get right sum
        for j in range(i + 1, n):
            rightsum += arr[j]

        # if leftsum and rightsum are same,
        # then we are done
        if leftsum == rightsum:
            return i

    # return -1 if no equilibrium index is found
    return -1

# driver code
arr = [-7, 1, 5, 2, -4, 3, 0]
print (equilibrium(arr))

# This code is contributed by Abhishek Sharama
```

**Output**

```
3
```

**时间复杂度:** O(n^2)

**方法二(刁钻高效)**
思路是先得到阵的总和。然后迭代数组并不断更新初始化为零的左和。在循环中，我们可以通过逐个减去元素得到正确的和。感谢 Sambasiva 提出了这个解决方案，并为此提供了代码。

```
1) Initialize leftsum  as 0
2) Get the total sum of the array as *sum*
3) Iterate through the array and for each index i, do following.
    a)  Update *sum* to get the right sum.  
           *sum* = *sum* - arr[i] 
       // *sum* is now right sum
    b) If leftsum is equal to *sum*, then return current index. 
       // update leftsum for next iteration.
    c) leftsum = leftsum + arr[i]
4) return -1 
// If we come out of loop without returning then
// there is no equilibrium index
```

下图显示了上述方法的试运行:

![](img/f62f31ef22a6773a833185b8c3bebc36.png)

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to find the equilibrium
# index of an array

# function to find the equilibrium index
def equilibrium(arr):

    # finding the sum of whole array
    total_sum = sum(arr)
    leftsum = 0
    for i, num in enumerate(arr):

        # total_sum is now right sum
        # for index i
        total_sum -= num

        if leftsum == total_sum:
            return i
        leftsum += num

      # If no equilibrium index found, 
      # then return -1
    return -1

# Driver code
arr = [-7, 1, 5, 2, -4, 3, 0]
print ('First equilibrium index is ',
       equilibrium(arr))

# This code is contributed by Abhishek Sharma
```

**Output**

```
First equilibrium index is 3
```

**产量:**
第一均衡指数为 3

**时间复杂度:** O(n)

**方法 3 :**

这是一个非常简单直接的方法。想法是取数组的前缀和两次。一个来自阵列前端，另一个来自阵列后端。

在获取两个前缀和之后，运行一个循环并检查一些 I，如果一个数组的两个前缀和等于第二个数组的前缀和，那么该点可以被认为是平衡点。

## 蟒蛇 3

```
# Python program to find the equilibrium
# index of an array

# Function to find the equilibrium index
def equilibrium(arr):
    left_sum = []
    right_sum = []

    # Iterate from 0 to len(arr)
    for i in range(len(arr)):

        # If i is not 0
        if(i):
            left_sum.append(left_sum[i-1]+arr[i])
            right_sum.append(right_sum[i-1]+arr[len(arr)-1-i])
        else:
            left_sum.append(arr[i])
            right_sum.append(arr[len(arr)-1])

    # Iterate from 0 to len(arr)    
    for i in range(len(arr)):
        if(left_sum[i] == right_sum[len(arr) - 1 - i ]):
            return(i)

    # If no equilibrium index found,then return -1
    return -1

# Driver code
arr = [-7, 1, 5, 2, -4, 3, 0]
print('First equilibrium index is ',
      equilibrium(arr))

# This code is contributed by Lokesh Sharma
```

**Output**

```
First Point of equilibrium is at index 3
```

**时间复杂度:** O(N)

**空间复杂度:** O(N)

更多详情请参考完整文章[数组平衡指数](https://www.geeksforgeeks.org/equilibrium-index-of-an-array/)！