# 打印给定字符串中插入数字 X 形成的最大整数

> 原文:[https://www . geesforgeks . org/print-给定字符串中插入数字 x 形成的最大整数/](https://www.geeksforgeeks.org/print-the-largest-integer-formed-by-inserting-digit-x-in-given-string/)

给定一个代表大整数值的大小为 **N** 的[字符串](https://www.geeksforgeeks.org/python-strings/) **S** ，以及一个正数 **X** ，任务是打印字符串 **S** 中插入数字 **X** 形成的最大整数。

**示例:**

> **输入:**S =“99”，X = 9
> **输出:** 999
> **说明:**
> 在“99”中插入 9 后能形成的最大数字是 999。
> 
> **输入:**S =“-13”，X = 2
> **输出:** -123
> **说明:**
> 在“-13”中插入 2 后能形成的最大数字是-123。

**方法:**这个问题可以通过[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符来解决。按照以下步骤解决此问题:

*   如果数字 **S** 为正，则执行以下步骤:
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤 **:**
        *   如果 **S[i]** 小于 **X** ，则在 **S[i]** 和**前插入数字 **X** ，断开**回路**。**
    *   如果以上情况都不满足，则在[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 的末尾追加数字 **X** 。
*   否则，如果数字 **S** 为负，则执行以下步骤:
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
        *   如果 **S[i]** 小于 **X** ，则在 **S[i]** 和**前插入数字 **X** ，断开**回路。
    *   如果以上情况都不满足，则在[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 的末尾追加数字 **X** 。
*   最后，打印最大可能的字符串，用 **S** 表示。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Function to find Largest Number after
# insertion of a digit
def largestValue(S, X):

    # If S is negative
    if S[0] == '-':
        f = 0
        # Iterate through characters of S
        for i, val in enumerate(S):
            if i == 0:
                continue

            # If digit x is less
            # than S[i] insert digit
            # after X
            if X < int(val):
                f = 1
                S = S[:i] + str(X) + S[i:]
                break

        if f == 0:
            S = S + str(X)

    # If S is positive
    else:
        f = 0

        # If x > S[i] insert x
        for i, val in enumerate(S):
            if X > int(val):
                f = 1
                S = S[:i] + str(X) + S[i:]
                break

        if f == 0:
            S = S + str(X)

    # Return the answer
    return S

# Driver Code

# Given Input
S = "-13"
X = 2

# Funtion Call
print(largestValue(S, X))
```

**Output**

```
-123
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)