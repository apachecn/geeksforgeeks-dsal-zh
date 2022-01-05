# 根据给定条件确定最大 1s 子序列的最小步骤

> 原文:[https://www . geeksforgeeks . org/基于给定条件确定最大 1s 子序列的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-determine-the-subsequence-with-max-1s-based-on-given-conditions/)

给定一个由“0”、“1”和“？”组成的大小为 **N** 的字符串 **S** ，其中 **N** 总是偶数。将字符串分成两个不同的字符串，比如 **S1** 和 **S2** ，其中 **S1** 将只包含**偶数**索引处的字符 **S** 和 **S2** 将只包含**奇数**索引处的字符 **S** 。任务是找到预测两个字符串 **S1** 和 **S2** 中哪一个的**最大**计数为 1 所需的**最小**可能步骤。在一个步骤中，为 **S1** 或 **S2 选择一个字符。**如果人物是“ **0** ”那么选“ **0** ”，如果人物是“ **1** ”那么选“ **1** ”，如果人物是“**？**然后选择 **1** 或 **0** 中的任意一个。

**示例:**

> **输入:** s =？10?0?"
> **输出:** 4
> **解释:**
> 第一步:S1 角色选择的是 S[0]= '？'，因此选择“0”。S1 =“0”，S2 =“0”。
> 第二步:对于 S2 角色选择的是 S[1]='1 '，所以选择' 1 '。S1 =“0”，S2 =“1”。
> 第一步:S1 角色选择是 S[2]= '？，因此选择“0”。S1 =“00”，S2 =“1”。
> 第一步:S1 角色选择是 S[3]= '？，所以选择‘1’。S1 =“00”，S2 =“11”。
> 在步骤 4 之后，S2 将有更多数量的 1，而不管剩余的索引选择什么数量。
> 
> **输入:** s =？1?0?？0110”
> T3】输出: 7

**方法:**思路是递归[解决问题](https://www.geeksforgeeks.org/recursion/)，探索所有可能的结果后回答这个问题。现在，要解决这个问题，请遵循以下步骤:

1.  创建一个名为**的函数，该函数包含参数、字符串 **S** 、指针 **i** ,该指针将指向字符串中的当前位置，直到字符串被分割为止；整数 **count1** 和 **count2** ,该整数将存储 1 的数量，直到 **i** 分别位于 **S1** 和 **S2** ， 整数**第一个**和**第二个**用于存储未选择值的 **S1** 和 **S2** 中的可用位置，整数 **n** 表示字符串的大小 **S** 。 该函数将返回预测答案所需的最小步骤。**
2.  现在最初，当前指针为零，因此 **i=0** 。由于到目前为止 **S1** 和 **S2** 都没有选择数值，并且 **S1** 和 **S2** 的所有地方都可以填充，因此 **count1=0** 、 **count2=0** 、 **first = n/2** 和 **second=n/2** 。所以，现在用这些参数调用函数 **minSteps** 。
3.  在函数**的每次调用中，分步骤**:
    *   检查基本案例，即:
        *   如果 **i** 到达 **n** (即 **i=n** )因为这意味着 **S1** 和 **S2** 都是满的，现在答案肯定可以预测。所以，返回 0。
        *   如果**计数 1** 变得大于**秒**和**计数 2** 之和，那么返回 0，因为现在，即使在 **S2** 中选择了所有可用位置的 1 之后， **S1** 将会有更多的 1。
        *   由于上述原因，如果**计数 2** 变得大于**第一**和**计数 1** 然后的总和，则返回 0。
    *   检查基本情况后，检查 **i** 是偶数还是奇数。如果 **i** 是偶数，那么这个指数被 **S1** 选择，否则 **S2** 选择。
    *   因此，根据当前正在填充的字符串递减**第一个**或**第二个**，因为填充后该字符串中的可用位置将减少一个位置。
    *   如果当前字符是“？”(即 **s[i] = '？'**)然后进行选择‘1’和选择‘0’的递归调用，并在向它们添加 1 之后返回两者中的最小值。
    *   否则，只需打一个电话，然后添加一个电话后返回答案。
4.  最后一次递归调用将给出这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

//// Recursive function to minimum steps
// required after combining two strings
int minSteps(string& S, int i, int count1, int count2,
             int first, int second, int n)
{
    // If current pointer reaches the end
    if (i == n) {
        return 0;
    }

    // Condition to conclude that one string does
    // more ones than the other irrespective of what
    // number is chosen for the remaining indexes
    if (count1 > (second + count2)
        || count2 > (first + count1)) {
        return 0;
    }

    int c1 = 0, c2 = 0;

    // If i is even, then choosing character for S1
    if (i % 2 == 0) {
        if (S[i] == '?') {
            return min(
                1
                    + minSteps(
                          S, i + 1,
                          count1 + 1, count2,
                          first - 1, second, n),
                1
                    + minSteps(
                          S, i + 1, count1, count2,
                          first - 1, second, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1 + 1, count2,
                       first - 1, second, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2,
                       first - 1, second, n);
            return c2;
        }
    }

    // If i is odd
    else {
        if (S[i] == '?') {
            return min(
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2 + 1,
                          first, second - 1, n),
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2,
                          first, second - 1, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2 + 1,
                       first, second - 1, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1, count1,
                       count2, first,
                       second - 1, n);
            return c2;
        }
    }
}

// Driver Code
int main()
{
    string s = "?10?0?";
    int N = s.size();

    cout << minSteps(s, 0, 0, 0,
                     N / 2, N / 2, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

//// Recursive function to minimum steps
// required after combining two strings
static int minSteps(String S, int i, int count1, int count2,
             int first, int second, int n)
{
    // If current pointer reaches the end
    if (i == n) {
        return 0;
    }

    // Condition to conclude that one string does
    // more ones than the other irrespective of what
    // number is chosen for the remaining indexes
    if (count1 > (second + count2)
        || count2 > (first + count1)) {
        return 0;
    }

    int c1 = 0, c2 = 0;

    // If i is even, then choosing character for S1
    if (i % 2 == 0) {
        if (S.charAt(i) == '?') {
            return Math.min(
                1
                    + minSteps(
                          S, i + 1,
                          count1 + 1, count2,
                          first - 1, second, n),
                1
                    + minSteps(
                          S, i + 1, count1, count2,
                          first - 1, second, n));
        }
        else if (S.charAt(i) == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1 + 1, count2,
                       first - 1, second, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2,
                       first - 1, second, n);
            return c2;
        }
    }

    // If i is odd
    else {
        if (S.charAt(i) == '?') {
            return Math. min(
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2 + 1,
                          first, second - 1, n),
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2,
                          first, second - 1, n));
        }
        else if (S.charAt(i) == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2 + 1,
                       first, second - 1, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1, count1,
                       count2, first,
                       second - 1, n);
            return c2;
        }
    }
}

// Driver code
public static void main (String[] args)
{
    String s = "?10?0?";
    int N = s.length();

    System.out.println(minSteps(s, 0, 0, 0,
                     N / 2, N / 2, N));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python code for the above approach
import math

# Recursive function to minimum steps
# required after combining two strings
def minSteps(S,  i,  count1,  count2,
             first,  second,  n):

    # If current pointer reaches the end
    if i == n:
        return 0

    # Condition to conclude that one string does
    # more ones than the other irrespective of what
    # number is chosen for the remaining indexes
    if count1 > second + count2 or count2 > first + count1:

        return 0

    c1 = 0
    c2 = 0

    # If i is even, then choosing character for S1
    if i % 2 == 0:
        if S[i] == '?':
            return min(
                1 + minSteps(
                    S, i + 1,
                    count1 + 1, count2,
                    first - 1, second, n),
                1 + minSteps(
                    S, i + 1, count1, count2,
                    first - 1, second, n))

        elif S[i] == '1':
            c1 = 1 + minSteps(
                S, i + 1,
                count1 + 1, count2,
                first - 1, second, n)
            return c1

        else:
            c2 = 1 + minSteps(
                S, i + 1,
                count1, count2,
                first - 1, second, n)
            return c2

    # If i is odd
    else:
        if S[i] == '?':
            return min(
                1 + minSteps(
                    S, i + 1,
                    count1, count2 + 1,
                    first, second - 1, n),
                1 + minSteps(
                    S, i + 1,
                    count1, count2,
                    first, second - 1, n))

        elif S[i] == '1':
            c1 = 1 + minSteps(
                S, i + 1,
                count1, count2 + 1,
                first, second - 1, n)
            return c1

        else:
            c2 = 1 + minSteps(
                S, i + 1, count1,
                count2, first,
                second - 1, n)
            return c2

# Driver Code
s = "?10?0?"
N = len(s)

print(minSteps(s, 0, 0, 0,
               math.floor(N / 2), math.floor(N / 2), N))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

//// Recursive function to minimum steps
// required after combining two strings
static int minSteps(string S, int i, int count1, int count2,
             int first, int second, int n)
{

    // If current pointer reaches the end
    if (i == n) {
        return 0;
    }

    // Condition to conclude that one string does
    // more ones than the other irrespective of what
    // number is chosen for the remaining indexes
    if (count1 > (second + count2)
        || count2 > (first + count1)) {
        return 0;
    }

    int c1 = 0, c2 = 0;

    // If i is even, then choosing character for S1
    if (i % 2 == 0) {
        if (S[i] == '?') {
            return Math.Min(
                1
                    + minSteps(
                          S, i + 1,
                          count1 + 1, count2,
                          first - 1, second, n),
                1
                    + minSteps(
                          S, i + 1, count1, count2,
                          first - 1, second, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1 + 1, count2,
                       first - 1, second, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2,
                       first - 1, second, n);
            return c2;
        }
    }

    // If i is odd
    else {
        if (S[i] == '?') {
            return Math.Min(
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2 + 1,
                          first, second - 1, n),
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2,
                          first, second - 1, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2 + 1,
                       first, second - 1, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1, count1,
                       count2, first,
                       second - 1, n);
            return c2;
        }
    }
}

// Driver code
public static void Main ()
{
    string s = "?10?0?";
    int N = s.Length;

    Console.Write(minSteps(s, 0, 0, 0,
                     N / 2, N / 2, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

//// Recursive function to minimum steps
// required after combining two strings
function minSteps(S, i, count1, count2,
             first, second, n)
{
    // If current pointer reaches the end
    if (i == n) {
        return 0;
    }

    // Condition to conclude that one string does
    // more ones than the other irrespective of what
    // number is chosen for the remaining indexes
    if (count1 > (second + count2)
        || count2 > (first + count1)) {
        return 0;
    }

    let c1 = 0, c2 = 0;

    // If i is even, then choosing character for S1
    if (i % 2 == 0) {
        if (S[i] == '?') {
            return Math.min(
                1
                    + minSteps(
                          S, i + 1,
                          count1 + 1, count2,
                          first - 1, second, n),
                1
                    + minSteps(
                          S, i + 1, count1, count2,
                          first - 1, second, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1 + 1, count2,
                       first - 1, second, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2,
                       first - 1, second, n);
            return c2;
        }
    }

    // If i is odd
    else {
        if (S[i] == '?') {
            return Math.min(
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2 + 1,
                          first, second - 1, n),
                1
                    + minSteps(
                          S, i + 1,
                          count1, count2,
                          first, second - 1, n));
        }
        else if (S[i] == '1') {
            c1 = 1
                 + minSteps(
                       S, i + 1,
                       count1, count2 + 1,
                       first, second - 1, n);
            return c1;
        }
        else {
            c2 = 1
                 + minSteps(
                       S, i + 1, count1,
                       count2, first,
                       second - 1, n);
            return c2;
        }
    }
}

// Driver Code
let s = "?10?0?";
let N = s.length;

document.write(minSteps(s, 0, 0, 0,
                     N / 2, N / 2, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
4
```

**时间复杂度:**o(2^n)
T3】辅助空间: O(1)