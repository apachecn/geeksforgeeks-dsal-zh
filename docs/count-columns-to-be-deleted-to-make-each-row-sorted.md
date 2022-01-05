# 统计要删除的列，对每一行进行排序

> 原文:[https://www . geesforgeks . org/count-待删除列-按行排序/](https://www.geeksforgeeks.org/count-columns-to-be-deleted-to-make-each-row-sorted/)

给定一个相同长度字符串的数组 **arr[]** ，任务是计算要删除的列数，以便对所有行进行字典排序。

**示例:**

> **输入:** arr[] = {“你好”、“极客”}
> **输出:** 1
> 删除第 1 列(索引 0)
> 现在两个字符串都按照字典顺序排序，即“ello”和“eeks”。
> 
> **输入:**arr[]= {“XYZ”、“lmn”、“pqr”}
> **输出:** 0
> 所有行都已经按字典顺序排序。

**做法:**问题的思路是找到要保留的列，而不是要删除的列。最后，我们返回计数值与字符串长度的差值。
现在，假设我们保留第一列 **C1** 。下一列 **C2** 对于 **i** 的所有有效值，我们必须将所有行按字典顺序排序，即**C1【I】<= C2【I】**，我们说已经删除了 **C1** 和 **C2** 之间的所有列。

下面是上述方法的实现:

```
# Python3 implementation of the approach

# Function to find minimum columns to be deleted
def deleteColumns(A):

    # Length of each string
    l = len(A[0])

    # Initialize dp array
    dp = [1] * l

    for i in range(l - 2, -1, -1):
        for j in range(i + 1, l):
            if all(row[i] <= row[j] for row in A):
                dp[i] = max(dp[i], 1 + dp[j])

    # Return result
    return l - max(dp)

# Driver Code
arr = ["hello", "geeks"]

# Function call to print required answer
print(deleteColumns(arr))
```

**Output:**

```
1

```