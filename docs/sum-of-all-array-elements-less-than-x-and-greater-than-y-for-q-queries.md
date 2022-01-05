# Q 查询所有小于 X 大于 Y 的数组元素之和

> 原文:[https://www . geeksforgeeks . org/所有数组元素之和-小于 x 大于 y-用于 q 查询/](https://www.geeksforgeeks.org/sum-of-all-array-elements-less-than-x-and-greater-than-y-for-q-queries/)

给定一个排序数组 **arr[]，**和一个具有 **M** 查询的集合 **Q** ，其中每个查询都有值 **X** 和 **Y** ，任务是找出数组中所有小于 **X** 且大于 **Y** 的整数之和。
**注意:**数组中可能有也可能没有 X 和 Y。

**示例:**

> **输入:** arr[] = [3 5 8 12 15]，Q = {{5，12}，{4，8}}
> **输出:**
> 18
> 30
> **解释:**
> 对于查询 1，X = 5，Y = 12。总和= 3( < 5) + 15( > 12) = 18。
> 对于查询 2，X = 4，Y = 8。总和= 3(<4)+15(>8)+12(>8)= 30。
> 
> **输入:** arr[] = [4 7 7 12 15]，Q = {{3，8}，{4，8}}
> **输出:**
> 27
> 27
> **说明:**
> 为查询 1，X = 3 且 Y = 8。总和= 12( > 8) + 15 ( > 8) = 27。
> 对于查询 2，Sum = 12 + 15 = 27。

**进场:**

1.  构建一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，其中**前缀 _ 和**表示 **arr[0] + arr[1] + … arr[i]** 的和。
2.  找到最后一个索引 **i** ，其值小于 **X** ，并提取前缀 sum 到 **i <sup>th</sup>** 索引。在 Python 和 C++中分别使用 [**平分 _left()**](https://www.geeksforgeeks.org/bisect-algorithm-functions-in-python/) 或[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)可以在 *O(logN)* 复杂度中获取索引..
3.  同样，找到数组中第一个索引 **i** ，其值大于 Y，并计算总和**prefix _ sum[n-1]–prefix _ sum[I-1]**。Python 和 C++中的内置函数[分别对分()](https://www.geeksforgeeks.org/binary-search-bisect-in-python/)和[上限()](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)，在 *O(logN)* 中执行所需操作。
4.  以上两个步骤计算出的两个结果之和即为所需答案。对每个查询重复这些步骤。

以下是上述方法的实现:

## 蟒蛇 3

```
# Python code for the above program
from bisect import bisect, bisect_left

def createPrefixSum(ar, n):

    # Initialize prefix sum 
    # array
    prefix_sum = [0]*n

    # Initialize prefix_sum[0]
    # by ar[0]
    prefix_sum[0] = ar[0]

    # Compute prefix sum for
    # all indices    
    for i in range(1, n):
        prefix_sum[i] = prefix_sum[i-1]+ar[i]
    return prefix_sum

# Function to return sum of all
# elements less than X
def sumLessThanX(ar, x, prefix_xum):

    # Index of the last element 
    # which is less than x
    pos_x = bisect_left(ar, x) - 1

    if pos_x >= 0 :
        return prefix_sum[pos_x]
    # If no element is less than x
    else:
        return 0

# Function to return sum of all
# elements greater than Y
def sumGreaterThanY(ar, y, prefix_sum):

    # Index of the first element 
    # which is greater than y
    pos_y = bisect(ar, y)
    pos_y -= 1

    if pos_y < len(ar)-1 :
        return prefix_sum[-1]-prefix_sum[pos_y]
    # If no element is greater than y
    else:
        return 0

def solve(ar, x, y, prefix_sum):
    ltx = sumLessThanX(ar, x, prefix_sum)
    gty = sumGreaterThanY(ar, y, prefix_sum)

    # printing the final sum
    print(ltx + gty) 

def print_l(lb, ub):
    print("sum of integers less than {}".format(lb)
    + " and greater than {} is ".format(ub),
    end = '')

if __name__ == '__main__':

    # example 1
    ar = [3, 6, 6, 12, 15]
    n = len(ar)
    prefix_sum = createPrefixSum(ar, n)

    # for query 1
    q1x = 5
    q1y = 12
    print_l(q1x, q1y)
    solve(ar, q1x, q1y, prefix_sum)

    # for query 2
    q2x = 7
    q2y = 8
    print_l(q2x, q2y)
    solve(ar, q2x, q2y, prefix_sum)
```

**Output:**

```
sum of integers less than 5 and greater than 12 is 18
sum of integers less than 7 and greater than 8 is 42

```

 ***时间复杂度:** O(N + (M * logN))
**辅助空间复杂度:** O(N)*