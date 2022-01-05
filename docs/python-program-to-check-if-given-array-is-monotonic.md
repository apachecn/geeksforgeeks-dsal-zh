# 检查给定数组是否单调的 Python 程序

> 原文:[https://www . geesforgeks . org/python-程序检查给定数组是否单调/](https://www.geeksforgeeks.org/python-program-to-check-if-given-array-is-monotonic/)

给定一个包含整数 T2 的数组。任务是检查数组是否为**单调**。如果数组是**单调递增**或**单调递减**，则数组是单调的。
如果对于所有 i < = j，**A【I】<= A【j】**，数组 A 是单调递增的。如果对于所有 i < = j，**A【I】>= A【j】**，数组 A 是单调递减的。
返回“**真**”如果给定数组 A 是单调的，则返回“**假**”(不带引号)。

示例:

```
Input : 6 5 4 4
Output : true

Input : 5 15 20 10
Output : false

```

**方法:**
一个数组是**单调的**当且仅当它是**单调递增**或**单调递减**。因为 **p < = q** 和 **q < = r** 意味着 **p < = r** 。所以我们只需要检查相邻的元素，分别确定数组是单调递增(还是单调递减)。我们可以一次检查这些属性。
要检查数组 A 是否为**单调递增**，我们将检查从 0 到 len(A)-2 的所有 I 索引的 **A[i] < = A[i+1]** 。同样，我们可以检查**单调递减**，其中 **A[i] > = A[i+1]** 用于从 0 到 len(A)-2 的所有 I 索引。
**注:**带**单元素的数组**可以认为既是**单调递增也是单调递减**，因此返回“**真**”。

**以下是上述方法的实施:**

## 蟒蛇 3

```
# Python3 program to find sum in Nth group

# Check if given array is Monotonic
def isMonotonic(A):

    return (all(A[i] <= A[i + 1] for i in range(len(A) - 1)) or
            all(A[i] >= A[i + 1] for i in range(len(A) - 1)))

# Driver program
A = [6, 5, 4, 4]

# Print required result
print(isMonotonic(A))

# This code is written by
# Sanjit_Prasad
```

Output:

```
True
```

**时间复杂度:** O(N)，其中 N 为数组长度。