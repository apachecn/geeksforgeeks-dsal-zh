# 交替重复删除奇数和偶数索引元素后，找到最后剩余的元素

> 原文:[https://www . geeksforgeeks . org/find-重复移除奇数和偶数索引元素后最后剩余的元素-交替/](https://www.geeksforgeeks.org/find-the-last-remaining-element-after-repeated-removal-of-odd-and-even-indexed-elements-alternately/)

给定正整数 **N** ，任务是在按照给定顺序交替重复执行以下操作后，打印序列**【1，N】**中的最后一个剩余元素:

1.  从序列中移除所有奇数索引的元素。
2.  从序列中移除所有偶数索引的元素。

**示例:**

> **输入:** N = 9
> **输出:** 6
> **解释:**
> 序列= {1，2，3，4，5，6，7，8，9}
> 步骤 1:移除奇数索引元素将序列修改为{2，4，6，8}
> 步骤 2:移除偶数索引元素将序列修改为{2，6}
> 步骤 3:移除奇数索引元素将序列修改为{6}
> 因此，最后一个
> 
> **输入:** N = 5
> **输出:** 2
> **解释:**
> 序列= {1，2，3，4，5}
> 步骤 1:移除奇数索引元素将序列修改为{2，4}
> 步骤 2:移除偶数索引元素将序列修改为{2}
> 因此，最后剩余的元素是 2。

**天真方法:**最简单的方法是将从 **1** 到 **N** 的所有元素按顺序存储在一个数组中。对于每个操作，从数组中移除元素，并将剩余的元素向左移动。将数组简化为单个元素后，将剩余的元素打印为所需的答案。

***时间复杂度:**O(N<sup>2</sup>* log N)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。
循环关系如下:

> ![dp[i] = 2*(1 + \frac{i}{2} - dp(\frac{i}{2})) ](img/f3ae02268548d008505ec9c1fbc4d8f0.png "Rendered by QuickLaTeX.com")
> 
> 其中， **i** 在范围【1，N】
> **DP【I】**存储数组元素从 1 到 I 时的答案

按照以下步骤解决问题:

1.  初始化一个数组 **dp[]** ，其中 **dp[i]** 存储剩余元素或序列**【1，I】**。
2.  对于 **i = 1** 的基础条件，打印 **1** 作为所需答案。
3.  使用前述递归关系计算**DP【N】**的值，并使用已经计算的子问题来避免重新计算[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。
4.  完成上述步骤后，打印**DP【N】**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the last
// remaining element from the sequence
int lastRemaining(int n, map<int, int> &dp)
{

    // If dp[n] is already calculated
    if (dp.find(n) != dp.end())
        return dp[n];

    // Base Case:
    if (n == 1)
        return 1;

    // Recursive call
    else
        dp[n] = 2 * (1 + n / 2 -
           lastRemaining(n / 2, dp));

    // Return the value of dp[n]
    return dp[n];
}

// Driver Code
int main()
{

    // Given N
    int N = 5;

    // Stores the
    map<int, int> dp;

    // Function call
    cout << lastRemaining(N, dp);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to calculate the last
// remaining element from the sequence
static int lastRemaining(int n, HashMap<Integer,
                                        Integer> dp)
{
  // If dp[n] is already calculated
  if (dp.containsKey(n))
    return dp.get(n);

  // Base Case:
  if (n == 1)
    return 1;

  // Recursive call
  else
    dp.put(n, 2 * (1 + n / 2 -
           lastRemaining(n / 2, dp)));

  // Return the value of dp[n]
  return dp.get(n);
}

// Driver Code
public static void main(String[] args)
{   
  // Given N
  int N = 5;

  // Stores the
  HashMap<Integer,
          Integer> dp = new HashMap<Integer,
                                    Integer>();

  // Function call
  System.out.print(lastRemaining(N, dp));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the last
# remaining element from the sequence
def lastRemaining(n, dp):

  # If dp[n] is already calculated
    if n in dp:
        return dp[n]

    # Base Case:
    if n == 1:
        return 1

    # Recursive Call
    else:
        dp[n] = 2*(1 + n//2
        - lastRemaining(n//2, dp))

    # Return the value of dp[n]
    return dp[n]

# Driver Code

# Given N
N = 5

# Stores the
dp = {}

# Function Call
print(lastRemaining(N, dp))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the last
// remaining element from the sequence
static int lastRemaining(int n, Dictionary<int,
                                           int> dp)
{

    // If dp[n] is already calculated
    if (dp.ContainsKey(n))
        return dp[n];

    // Base Case:
    if (n == 1)
        return 1;

    // Recursive call
    else
        dp.Add(n, 2 * (1 + n / 2 -
             lastRemaining(n / 2, dp)));

    // Return the value of dp[n]
    return dp[n];
}

// Driver Code
public static void Main(String[] args)
{ 

    // Given N
    int N = 5;

    // Stores the
    Dictionary<int,
               int> dp = new Dictionary<int,
                                        int>();

    // Function call
    Console.Write(lastRemaining(N, dp));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to calculate the last
      // remaining element from the sequence
      function lastRemaining(n, dp) {
        // If dp[n] is already calculated
        if (dp.hasOwnProperty(n))
            return dp[n];

        // Base Case:
        if (n === 1)
            return 1;
        // Recursive call
        else
          dp[n] =
            2 * (1 + parseInt(n / 2) -
            lastRemaining(parseInt(n / 2), dp));

        // Return the value of dp[n]
        return dp[n];
      }

      // Driver Code
      // Given N
      var N = 5;

      // Stores the
      var dp = {};

      // Function call
      document.write(lastRemaining(N, dp));
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)