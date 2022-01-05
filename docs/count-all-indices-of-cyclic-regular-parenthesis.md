# 计算循环正则括号

的所有指数

> 原文:[https://www . geesforgeks . org/count-all-indexes-of-cyclic-正则括号/](https://www.geeksforgeeks.org/count-all-indices-of-cyclic-regular-parenthesis/)

给定一个长度为 **N** 的字符串 **S** ，仅由左括号“ **(** )和右括号“ **)** ”组成。任务是找到所有的索引“ **K** ”，这样 **S[K…N-1] + S[0…K-1]** 就是一个正则括号。

> 一个**常规括号**字符串或者为空 **("")** 、**”(“+str1+”)“**，或者 **str1 + str2** ，其中 str 1 和 str2 为常规括号字符串。
> 例如:**“**”、**“()”**、**“())()”**、**“()(()))”**都是常规的括号字符串。

**例:**

> **输入:**str =()(“
> **输出:** 2
> **解释:**
> 对于 K = 1，S =()()，这是有规律的。
> 对于 K = 3，S =()()，这是有规律的。
> **输入:**S =()(“
> **输出:** 1
> **解释:**
> 对于 K = 3，S =(())，这是有规律的。

**朴素方法:**朴素方法是在每个可能的索引处拆分给定的字符串 **str** (比如说 **K** )并检查**str【K，N-1】+str【0，K-1】**是否回文。如果是，则打印 **K** 的特定值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效方法:**想法是观察如果在任意一个索引(比如说 **K** )中，闭括号的计数大于开括号的计数，那么该索引就是拆分字符串的可能索引。以下是步骤:

1.  只有当左括号的数量必须等于右括号的数量时，分区才是可能的。否则我们不能形成任何分区来平衡括号。
2.  创建一个字符串大小长度的辅助数组(比如 **aux[]** )。
3.  如果任意索引处的字符(比如说 **i** )是**(“**)则遍历给定的字符串，然后将 **aux[i]更新为 1** 否则将强> aux[i]更新为-1。
4.  上述辅助数组中最小元素的频率是使 **S[K…N-1] + S[0…K-1]** 成为规则括号串所需的拆分次数(比如在索引 **K** 处)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all indices which
// cyclic shift leads to get
// balanced parenthesis
int countCyclicShifts(string& S, int n)
{
    int aux[n] = { 0 };

    // Create auxiliary array
    for (int i = 0; i < n; ++i) {
        if (S[i] == '(')
            aux[i] = 1;
        else
            aux[i] = -1;
    }

    // Finding prefix sum and
    // minimum element
    int mn = aux[0];

    for (int i = 1; i < n; ++i) {
        aux[i] += aux[i - 1];

        // Update the minimum element
        mn = min(mn, aux[i]);
    }

    // ChecK if count of '(' and
    // ')' are equal
    if (aux[n - 1] != 0)
        return 0;

    // Find count of minimum
    // element
    int count = 0;

    // Find the frequency of mn
    for (int i = 0; i < n; ++i) {
        if (aux[i] == mn)
            count++;
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    // Given string S
    string S = ")()(";

    int N = S.length();

    // Function Call
    cout << countCyclicShifts(S, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find all indices which
// cyclic shift leads to get
// balanced parenthesis
static int countCyclicShifts(String S, int n)
{

    // Create auxiliary array
    int[] aux = new int[n];

    for(int i = 0; i < n; ++i)
    {
       if (S.charAt(i) == '(')
           aux[i] = 1;
       else
           aux[i] = -1;
    }

    // Finding prefix sum and
    // minimum element
    int mn = aux[0];

    for(int i = 1; i < n; ++i)
    {
       aux[i] += aux[i - 1];

       // Update the minimum element
       mn = Math.min(mn, aux[i]);
    }

    // Check if count of '(' and ')'
    // are equal
    if (aux[n - 1] != 0)
        return 0;

    // Find count of minimum
    // element
    int count = 0;

    // Find the frequency of mn
    for(int i = 0; i < n; ++i)
    {
       if (aux[i] == mn)
           count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void main(String[] args)
{

    // Given string S
    String S = ")()(";

    // length of the string S
    int N = S.length();

    System.out.print(countCyclicShifts(S, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all indices which
# cyclic shift leads to get
# balanced parenthesis
def countCyclicShifts(S, n):

    aux = [0 for i in range(n)]

    # Create auxiliary array
    for i in range(0, n):
        if (S[i] == '('):
            aux[i] = 1
        else:
            aux[i] = -1

    # Finding prefix sum and
    # minimum element
    mn = aux[0]

    for i in range(1, n):
        aux[i] += aux[i - 1]

        # Update the minimum element
        mn = min(mn, aux[i])

    # ChecK if count of '(' and
    # ')' are equal
    if (aux[n - 1] != 0):
        return 0

    # Find count of minimum
    # element
    count = 0

    # Find the frequency of mn
    for i in range(0, n):
        if (aux[i] == mn):
            count += 1

    # Return the count
    return count

# Driver Code

# Given string S
S = ")()("
N = len(S)

# Function call
print(countCyclicShifts(S, N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find all indices which
// cyclic shift leads to get
// balanced parenthesis
static int countCyclicShifts(string S, int n)
{

    // Create auxiliary array
    int[] aux = new int[n];

    for(int i = 0; i < n; ++i)
    {
        if (S[i] == '(')
            aux[i] = 1;
        else
            aux[i] = -1;
    }

    // Finding prefix sum and
    // minimum element
    int mn = aux[0];

    for(int i = 1; i < n; ++i)
    {
        aux[i] += aux[i - 1];

        // Update the minimum element
        mn = Math.Min(mn, aux[i]);
    }

    // Check if count of '(' and ')'
    // are equal
    if (aux[n - 1] != 0)
        return 0;

    // Find count of minimum
    // element
    int count = 0;

    // Find the frequency of mn
    for(int i = 0; i < n; ++i)
    {
        if (aux[i] == mn)
            count++;
    }

    // Return the count
    return count;
}

// Driver code
public static void Main(string[] args)
{

    // Given string S
    string S = ")()(";

    // length of the string S
    int N = S.Length;

    Console.Write(countCyclicShifts(S, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to find all indices which
// cyclic shift leads to get
// balanced parenthesis
function countCyclicShifts(S, n)
{

    // Create auxiliary array
    let aux = [];

    for(let i = 0; i < n; ++i)
    {
       if (S[i] == '(')
           aux[i] = 1;
       else
           aux[i] = -1;
    }

    // Finding prefix sum and
    // minimum element
    let mn = aux[0];

    for(let i = 1; i < n; ++i)
    {
       aux[i] += aux[i - 1];

       // Update the minimum element
       mn = Math.min(mn, aux[i]);
    }

    // Check if count of '(' and ')'
    // are equal
    if (aux[n - 1] != 0)
        return 0;

    // Find count of minimum
    // element
    let count = 0;

    // Find the frequency of mn
    for(let i = 0; i < n; ++i)
    {
       if (aux[i] == mn)
           count++;
    }

    // Return the count
    return count;
}

// Driver Code

    // Given string S
    let S = ")()(";

    // length of the string S
    let N = S.length;

    document.write(countCyclicShifts(S, N));   

// This code is contributed by avijitmondal1998.
</script>
```

**Output:**

```
2
```

**时间复杂度:** *O(N)* ，其中 N 是字符串的长度。
**辅助空间:** *O(N)* ，其中 N 为弦的长度。