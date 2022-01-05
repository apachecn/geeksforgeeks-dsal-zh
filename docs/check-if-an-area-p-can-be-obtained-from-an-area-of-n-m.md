# 检查从 N * M 的区域是否可以得到区域 P

> 原文:[https://www . geesforgeks . org/check-if-an-area-p-can-from-area-n-m/](https://www.geeksforgeeks.org/check-if-an-area-p-can-be-obtained-from-an-area-of-n-m/)

给定整数 **N** 、 **M** 和 **P** ，任务是检查是否有可能找到 **P** sq 的矩形区域。 **N × M** sq 单位矩形区域内的单位。

**示例:**

> I **nput:** N = 3，M = 3，P = 4
> **输出:** YES
> **说明:**2×2 sq 的矩形。单位面积
> 
> **输入:** N = 4，M = 4，P = 7
> T3】输出:否

**方法:**按照以下步骤解决问题

*   [找到 **p** 的所有因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)并存储在向量中，比如**因子**。
*   维持秩序 **N ≤ M** 。
*   [遍历](https://www.geeksforgeeks.org/vector-in-cpp-stl/)向量**因子**。
    *   对于每个数组元素**因子【I】**，检查**因子【I】≤N**和 **p /因子【I】≤M**，其中**因子【I】**和 **p /因子【I】**表示矩形区域的尺寸。
    *   如果发现是真的，打印**是**并返回。
*   否则，打印**否**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a rectangle
// of p sq units can be formed from
//  an area of n * m sq units
void splitArea(int n, int m, int p)
{
    // Maintain order n <= m
    if (n > m)
        swap(n, m);

    vector<int> factors;

    // Iterate to find factors of p
    for (int i = 1; i * i <= p; i++) {

        // p is divisible by i
        if (p % i == 0) {
            factors.push_back(i);
        }
    }

    for (int i = 0; i < (int)factors.size();
         i++) {

        // Check if dimensions
        // lie in given area
        if (factors[i] <= n &&
            p / factors[i] <= m) {

            cout << "YES";
            return;
        }
    }

    cout << "NO";
}

// Driver Code
int main()
{
    int n = 3, m = 3, p = 4;
    splitArea(n, m, p);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to swap two numbers
  // Using temporary variable
  static void swap(int m, int n)
  {

    // Swapping the values
    int temp = m;
    m = n;
    n = temp;
  }

  // Function to check if a rectangle
  // of p sq units can be formed from
  //  an area of n * m sq units
  static void splitArea(int n, int m, int p)
  {

    // Maintain order n <= m
    if (n > m)
      swap(n, m);
    ArrayList<Integer> factors = new ArrayList<Integer>();

    // Iterate to find factors of p
    for (int i = 1; i * i <= p; i++)
    {

      // p is divisible by i
      if (p % i == 0)
      {
        factors.add(i);
      }
    }

    for (int i = 0; i < (int)factors.size();
         i++)
    {

      // Check if dimensions
      // lie in given area
      if (factors.get(i) <= n &&
          p / factors.get(i) <= m)
      {
        System.out.print("YES");
        return;
      }
    }

    System.out.print("NO");
  }

// Driver code
public static void main(String[] args)
{
    int n = 3, m = 3, p = 4;
    splitArea(n, m, p);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a rectangle
# of p sq units can be formed from
# an area of n * m sq units
def splitArea(n, m, p):

    # Maintain order n <= m
    if (n > m):
        n, m = m, n
    factors = []

    # Iterate to find factors of p
    for i in range(1, p + 1):

        # p is divisible by i
        if (p % i == 0):
            factors.append(i)

    for i in range(len(factors)):

        # Check if dimensions
        # lie in given area
        if (factors[i] <= n and p // factors[i] <= m):
            print("YES")
            return

    print("NO")

# Driver Code
if __name__ == '__main__':
    n, m, p = 3, 3, 4
    splitArea(n, m, p)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to swap two numbers
  // Using temporary variable
  static void swap(int m, int n)
  {

    // Swapping the values
    int temp = m;
    m = n;
    n = temp;
  }

  // Function to check if a rectangle
  // of p sq units can be formed from
  //  an area of n * m sq units
  static void splitArea(int n, int m, int p)
  {

    // Maintain order n <= m
    if (n > m)
      swap(n, m);
    List<int> factors = new List<int>();

    // Iterate to find factors of p
    for (int i = 1; i * i <= p; i++)
    {

      // p is divisible by i
      if (p % i == 0)
      {
        factors.Add(i);
      }
    }

    for (int i = 0; i < (int)factors.Count;
         i++)
    {

      // Check if dimensions
      // lie in given area
      if (factors[i] <= n &&
          p / factors[i] <= m)
      {
        Console.Write("YES");
        return;
      }
    }

    Console.Write("NO");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int n = 3, m = 3, p = 4;
    splitArea(n, m, p);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to swap two numbers
      // Using temporary variable
      function swap(m, n) {
        // Swapping the values
        var temp = m;
        m = n;
        n = temp;
      }

      // Function to check if a rectangle
      // of p sq units can be formed from
      // an area of n * m sq units
      function splitArea(n, m, p) {
        // Maintain order n <= m
        if (n > m) swap(n, m);
        var factors = new Array();

        // Iterate to find factors of p
        for (var i = 1; i * i <= p; i++) {
          // p is divisible by i
          if (p % i == 0) {
            factors.push(i);
          }
        }

        for (var i = 0; i < factors.length; i++) {
          // Check if dimensions
          // lie in given area
          if (factors[i] <= n && p / factors[i] <= m) {
            document.write("YES");
            return;
          }
        }

        document.write("NO");
      }

      // Driver code
      var n = 3,
        m = 3,
        p = 4;
      splitArea(n, m, p);
    </script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(√P)*
***辅助空间:** O(log(P))*