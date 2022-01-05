# 数组中唯一对之间所有差异的最小和

> 原文:[https://www . geeksforgeeks . org/阵列中唯一对之间所有差异的最小和/](https://www.geeksforgeeks.org/minimum-sum-of-all-differences-between-unique-pairs-in-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在更新[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 后，找到[数组](https://www.geeksforgeeks.org/array-data-structure/)中唯一元素对之间所有绝对差的最小和。要更新[数组](https://www.geeksforgeeks.org/array-data-structure/)，可以按任意顺序选择数组中的任意两个元素。从第一个元素中减去 1，并添加到第二个元素中。这个步骤可以重复任何次数。

**示例:**

> **输入:** arr[]={1，2，3}
> **输出:** 0
> **说明:**选择 1 和 3 更新数组，3-1=2，1+1=2。所以更新后的数组变成了 arr[]={2，2，2}。对的绝对差的最小可能和是 0+0+0=0。
> 
> **输入:** arr[]={0，1，1，0}
> **输出:** 4
> **说明:**选择任意两个元素进行上升会导致绝对差总和增加。所以总和是 1+1+1+1+0+0=4。

**方法:**给定的问题可以基于以下观察来解决:

*   为了最小化所有唯一对之间的绝对差的总和，元素应该尽可能地接近。
*   为此，求总和 **S** 并将总和 **S** 除以 **N** ，即 **val = S/N.**
*   如果 **val** 是一个整数，那么问题就变得非常简单了，因为按照这些操作，所有的整数都可以转换成 **X** 。
*   否则，一些元素说 **X** 将是刚好小于 **val 的整数，**即**楼层(val)** 而其他的将是**天花板(val)。**
*   为了找到 **X 的值，**使用这样一个事实，即即使在更新之后，数组的和也将是相同的。所以，用下面的公式求 **X.** 的值

> x *(B- 1)+N * b–x * b = S
> 
> = > x * b–x+N * b–x * b = S
> 
> = > N * b–x = S
> 
> = >**x = N * b–S**

*   例如

> N = 10
> arr[] = {8，3，6，11，5，2，1，7，10，4}
> 数组所有元素之和，S=57
> 所以，S/N = 5.7 意味着如果所有元素都转换为 5.7，那么所有唯一元素对的所有绝对差 b/w 之和将被最小化，即 0。
> 但是使用上述操作将所有元素转换为 5.7 是不可能的。
> 所以，有些元素是 5，其他的是 6。
> 
> 现在，问题是有多少元素是 5。假设 x，那么(N-x)将是 6，在这个过程中，和将总是守恒的。
> =>x * 5+(N-x)* 6 = 57
> =>-x = 57–60(将 N 的值设为 10 并求解方程)
> -x = -3 = > x=3
> 因此，转换后的数组将是{5，5，5，6，6，6，6，6，6，6}

*   现在给出类似 1 的差值的对是 **x*(N-x)** 。
*   所以差的总和也将是 **x*(N-x)** 。

按照以下步骤解决问题:

*   将变量 **sum** 初始化为 **0** 以存储[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中元素的总和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将变量**之和中**arr【I】**的值相加。**
*   将变量**温度**初始化为**(浮动)信噪比**
*   将 **a** 的值设置为**温度的[楼层](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)值。**
*   将 **b** 的值设置为**温度的[上限](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)值。**
*   将 **x** 的值设置为 **b*N-sum** 来存储将要发生分区的位置。
*   打印 **x*(N-x)** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// sum of differences of pairs
void solve(int N, int arr[])
{
    int a, b, S = 0, x;
    for (int i = 0; i < N; i++) {
        // Take sum of all elements
        S = S + arr[i];
    }

    // Store s/n to a temporary float
    // variable and typecast
    // s/n to get exact float value
    float temp = (float)S / N;

    // take floor value of temp
    a = floor(temp);
    // take floor value of temp
    b = ceil(temp);
    // position where partition will happen
    x = b * N - S;
    // Total sum of differences
    cout << x * (N - x);
}

// Driver Code
int main()
{
    int arr[] = { 8, 3, 6, 11, 5, 2, 1, 7, 10, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    solve(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to calculate the minimum
// sum of differences of pairs
static void solve(int N, int arr[])
{
    int a, b, S = 0, x;
    for (int i = 0; i < N; i++)
    {

        // Take sum of all elements
        S = S + arr[i];
    }

    // Store s/n to a temporary float
    // variable and typecast
    // s/n to get exact float value
    float temp =(float) S / N;

    // take floor value of temp
    a = (int) Math.floor(temp);

    // take floor value of temp
    b = (int)Math.ceil(temp);

    // position where partition will happen
    x = b * N - S;

    // Total sum of differences
      System.out.println(x * (N - x));
}

// Driver Code
    public static void main (String[] args) {
       int arr[] = { 8, 3, 6, 11, 5, 2, 1, 7, 10, 4 };
    int N = arr.length;

    solve(N, arr);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to calculate the minimum
# sum of differences of pairs
def solve(N, arr):
    a, b, S, x = 0, 0, 0, 0;
    for i in range(0, N, 1):

        # Take sum of all elements
        S = S + arr[i];

    # Store s/n to a temporary float
    # variable and typecast
    # s/n to get exact float value
    temp = S / N;

    # take floor value of temp
    a = math.floor(temp);

    # take floor value of temp
    b = math.ceil(temp);

    # position where partition will happen
    x = b * N - S;

    # Total sum of differences
    print(x * (N - x));

# Driver Code
if __name__ == '__main__':
    arr = [ 8, 3, 6, 11, 5, 2, 1, 7, 10, 4 ];
    N = len(arr);

    solve(N, arr);

# This code is contributed by 29AjayKumar
```

## C#

```
using System;

public class GFG {
    static void solve(int N, int[] arr)
    {
        int  b, S = 0, x;
        for (int i = 0; i < N; i++) {

            // Take sum of all elements
            S = S + arr[i];
        }

        // Store s/n to a temporary float
        // variable and typecast
        // s/n to get exact float value
        float temp = (float)S / N;

        // take floor value of temp
        b = (int)Math.Ceiling(temp);

        // position where partition will happen
        x = b * N - S;

        // Total sum of differences
        Console.WriteLine(x * (N - x));
    }

    // Driver Code
    static public void Main()
    {
        int[] arr = { 8, 3, 6, 11, 5, 2, 1, 7, 10, 4 };
        int N = arr.Length;

        solve(N, arr);
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to calculate the minimum
// sum of differences of pairs
function solve(N, arr) {
  let a,
    b,
    S = 0,
    x;
  for (let i = 0; i < N; i++) {
    // Take sum of all elements
    S = S + arr[i];
  }

  // Store s/n to a temporary float
  // variable and typecast
  // s/n to get exact float value
  let temp = S / N;

  // take floor value of temp
  a = Math.floor(temp);
  // take floor value of temp
  b = Math.ceil(temp);
  // position where partition will happen
  x = b * N - S;
  // Total sum of differences
  document.write(x * (N - x));
}

// Driver Code

let arr = [8, 3, 6, 11, 5, 2, 1, 7, 10, 4];
let N = arr.length;

solve(N, arr);

// This code is contributed by gfgking.
</script>
```

**Output**

```
21
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)