# 最大产品子阵列的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python 3-最大产品计划-subarray/](https://www.geeksforgeeks.org/python3-program-for-maximum-product-subarray/)

给定一个包含正整数和负整数的数组，求最大乘积子数组的乘积。预期时间复杂度为 0(n)，只能使用 0(1)个额外空间。

**示例:**

```
Input: arr[] = {6, -3, -10, 0, 2}
Output:   180  // The subarray is {6, -3, -10}

Input: arr[] = {-1, -3, -10, 0, 60}
Output:   60  // The subarray is {60}

Input: arr[] = {-2, -40, 0, -2, -3}
Output:   80  // The subarray is {-2, -40}
```

**天真解决方案:**

其思想是遍历每个连续的子阵列，找到每个子阵列的乘积，并从这些结果中返回最大乘积。

下面是上述方法的实现。

## 蟒蛇 3

```
# Python3 program to find Maximum Product Subarray

# Returns the product of max product subarray.
def maxSubarrayProduct(arr, n):

    # Initializing result
    result = arr[0]

    for i in range(n):

        mul = arr[i]

        # traversing in current subarray
        for j in range(i + 1, n):

            # updating result every time
            # to keep an eye over the maximum product
            result = max(result, mul)
            mul *= arr[j]

        # updating the result for (n-1)th index.
        result = max(result, mul)

    return result

# Driver code
arr = [ 1, -2, -3, 0, 7, -8, -2 ]
n = len(arr)
print("Maximum Sub array product is" , maxSubarrayProduct(arr, n))

# This code is contributed by divyeshrabadiya07
```

**输出:**

```
Maximum Sub array product is 112
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**高效解决方案:**

下面的解决方案假设给定的输入数组总是有一个正输出。该解决方案适用于上述所有情况。它不适用于{0，0，-20，0}、{0，0，0}这样的数组..等等。可以很容易地修改解决方案来处理这种情况。
类似于[最大和邻接子阵](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)问题。这里唯一要注意的是，最大乘积也可以由以前一个元素结尾的最小(负)乘积乘以这个元素得到。例如，在数组{12，2，-3，-5，-6，-2}中，当我们位于元素-2 时，最大乘积是的乘积，最小乘积以-6 和-2 结尾。

## 蟒蛇 3

```
# Python program to find maximum product subarray

# Returns the product of max product subarray.
# Assumes that the given array always has a subarray
# with product more than 1
def maxsubarrayproduct(arr):

    n = len(arr)

    # max positive product ending at the current position
    max_ending_here = 1

    # min positive product ending at the current position
    min_ending_here = 1

    # Initialize maximum so far
    max_so_far = 0
    flag = 0

    # Traverse throughout the array. Following values
    # are maintained after the ith iteration:
    # max_ending_here is always 1 or some positive product
    # ending with arr[i]
    # min_ending_here is always 1 or some negative product
    # ending with arr[i]
    for i in range(0, n):

        # If this element is positive, update max_ending_here.
        # Update min_ending_here only if min_ending_here is
        # negative
        if arr[i] > 0:
            max_ending_here = max_ending_here * arr[i]
            min_ending_here = min (min_ending_here * arr[i], 1)
            flag = 1

        # If this element is 0, then the maximum product cannot
        # end here, make both max_ending_here and min_ending_here 0
        # Assumption: Output is alway greater than or equal to 1.
        elif arr[i] == 0:
            max_ending_here = 1
            min_ending_here = 1

        # If element is negative. This is tricky
        # max_ending_here can either be 1 or positive.
        # min_ending_here can either be 1 or negative.
        # next min_ending_here will always be prev.
        # max_ending_here * arr[i]
        # next max_ending_here will be 1 if prev
        # min_ending_here is 1, otherwise
        # next max_ending_here will be prev min_ending_here * arr[i]
        else:
            temp = max_ending_here
            max_ending_here = max (min_ending_here * arr[i], 1)
            min_ending_here = temp * arr[i]
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here

    if flag == 0 and max_so_far == 0:
        return 0
    return max_so_far

# Driver function to test above function
arr = [1, -2, -3, 0, 7, -8, -2]
print "Maximum product subarray is", maxsubarrayproduct(arr)

# This code is contributed by Devesh Agrawal
```

**Output**

```
Maximum Sub array product is 112
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

更多详情请参考[最大产品斯巴莱](https://www.geeksforgeeks.org/maximum-product-subarray/)整篇文章！