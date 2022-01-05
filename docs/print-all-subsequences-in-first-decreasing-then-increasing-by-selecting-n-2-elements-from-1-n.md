# 通过从[1，N]

中选择 N/2 个元素，以先减后增的方式打印所有子序列

> 原文:[https://www . geeksforgeeks . org/print-all-subseries-in-first-reduced-then-递增-selection-n-2-elements-from-1-n/](https://www.geeksforgeeks.org/print-all-subsequences-in-first-decreasing-then-increasing-by-selecting-n-2-elements-from-1-n/)

给定一个正整数 **N** ，任务是通过从 **1** 到 **N** 中选择 **ceil(N/2)** 元素，以先减后增的方式打印[数组](https://www.geeksforgeeks.org/array-data-structure/)的所有子序列。

**示例:**

> **输入:** N = 5
> **输出:**
> (2，1，3)，(2，1，4)，(2，1，5)，(3，1，2)，(3，1，4)，(3，1，5)，(3，2，4)，(3，2，5)，(4，1，2)，
> (4，1，3)，(4，1，5)，(4，2，3)，(4，2，5)，(4，2，5)，(4，3，5)，(5，1，2)，(5，1，3)，(5，5)，(5，3，5)
> 这些是大小为 3 的有效序列，先减少后增加。

**方法:**该方法基于使用 python 的内置函数[ITER tools . arrange](https://www.geeksforgeeks.org/python-itertools-permutations/)来生成大小 ceil(N/2)的所有子序列。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，插入从 **1** 到 **N** 的所有元素。
*   将变量 **K** 初始化为**上限(N/2)** 。
*   使用名为 [**的内置函数插入数组“**序列**中的所有子序列。**](https://www.geeksforgeeks.org/itertools-combinations-module-python-print-possible-combinations/)
*   [使用变量**序列**迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **序列**，并执行以下步骤:
    *   检查 **seq[1] > seq[0]** 或 **seq[-1] < seq[-2]** 或 **seq** 是增加还是减少，然后继续，否则该序列不满足上述条件。
    *   如果元素多于 **seq[i] < seq[i-1]** 和 **seq[i] < seq[i+1]** 那么也继续，不打印数组。
    *   如果**序列**没有遵循以上任何一点，则打印**序列**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

# import the ceil permutations in function 
from math import ceil

# Function to generate all the permutations
from itertools import permutations

# Function to check if the sequence is valid
# or not
def ValidSubsequence(seq):

  # If first element is greater or last second
  # element is greater than last element
  if (seq[0]<seq[1]) or (seq[-1]<seq[-2]): return False

  i = 0

  # If the sequence is decreasing or increasing
  # or sequence is increasing return false
  while i<len(seq)-1:
    if seq[i]>seq[i + 1]:
      pass
    elif seq[i]<seq[i + 1]:
      j = i + 1
      if (j != len(seq)-1) and (seq[j]>seq[j + 1]):
        return False
    i+= 1

   # If the sequence do not follow above condition
   # Return True
  return True 

# Driver code
N = 5
K = ceil(N / 2)
arr = list(range(1, N + 1))

# Generate all permutation of size N / 2 using
# default function
sequences = list(permutations(arr, K))

# Print the sequence which is valid valley subsequence
for seq in sequences:
  # Check whether the seq is valid or not 
  # Function Call
  if ValidSubsequence(seq):
    print(seq, end =" ")
```

**Output:**

```
(2, 1, 3) (2, 1, 4) (2, 1, 5) (3, 1, 2) (3, 1, 4) (3, 1, 5) (3, 2, 4) (3, 2, 5) (4, 1, 2) (4, 1, 3) (4, 1, 5) (4, 2, 3) (4, 2, 5) (4, 3, 5) (5, 1, 2) (5, 1, 3) (5, 1, 4) (5, 2, 3) (5, 2, 4) (5, 3, 4)

```

***时间复杂度:**O(C<sup>N</sup>T5】N/2* ceil(N/2)！*N)*
***辅助空间:**O(C<sup>N</sup><sub>N/2</sub>* ceil(N/2)！)*