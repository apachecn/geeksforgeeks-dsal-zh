# 使用 1 到 N 范围内的数字计算不同对之间的异或值

> 原文:[https://www . geeksforgeeks . org/count-distinct-xor-values-in-pair-使用 1 到 n 范围内的数字/](https://www.geeksforgeeks.org/count-distinct-xor-values-among-pairs-using-numbers-in-range-1-to-n/)

给定一个数字 **N** 。任务是使用从 **1** 到 **N** 的数字计算任何可能对的不同异或的数量。

**示例:**

> **输入:** N = 3
> **输出:** 4
> **解释:**以下是使用从 1 到 N(含 1 到 N)的元素的所有可能的对。
> 1^1 = 0
> 1^2 = 3
> 1^3 = 2
> 2^2 = 0
> 2^3 = 1
> 3^3 = 0
> 因此，有 4 个不同的可能异或值。
> 
> **输入:**N = 2
> T3】输出: 2

**方法:**这个问题是基于观察的。按照以下步骤解决给定的问题。

*   对于 **N = 1** 和 **N = 2** ，要求的输出分别为 **1** 和 **2** 。
*   现在对于 **N≥3** ，有两种可能的情况:
    *   如果 **N** 不是 2 的幂，那么将会有总共**个数字，其中 **t** 是 **2** 的幂，刚好在数字 **N** 旁边。它们从**【0 到 t–1】**不等。因为假设 **N = 5** 或 **6** 或 **7** 在上述所有情况下，数值都不同于**【0，1，2，3，4，5，6，7】**。**
    *   **如果 **N** 是 2 的幂，那么除了数字本身，所有的数字都是可能的。因为假设二进制中 **N = 4** 是***【100】***所以我们知道异或运算给出****1”**如果两个位都不同，那么它给出 *0* 。可能的值是**【0，1，2，3，** ~~**4**~~ **，5，6，7】**。****

****下面是上述方法的实现。****

## ****C++****

```
**// C++ code to implement above approach
#include <cmath>
#include <iostream>
using namespace std;

int findDistinctXOR(int n)
{

    // Corner case
    if (n == 1) {
        cout << 1 << endl;
    }
    if (n == 2) {
        cout << 2 << endl;
    }

    long long x, next;
    x = log2(n);

    // if n is power of two
    if ((n & (n - 1)) == 0) {

        next = pow(2, x + 1);
        cout << next - 1 << endl;
    }
    else {
        next = pow(2, x + 1);
        cout << next << endl;
    }
}

// Driver Code
int main()
{
    int N = 3;

    findDistinctXOR(N);
    return 0;
}**
```

## ****蟒蛇 3****

```
**# Python code for the above approach
import math as Math

def findDistinctXOR(n):

    # Corner case
    if (n == 1):
        print(1)
    if (n == 2):
        print(2)
    x = None
    next = None
    x = Math.floor(Math.log2(n))

    # if n is power of two
    if ((n & (n - 1)) == 0):
        next = Math.pow(2, x + 1)
        print((next - 1))
    else:
        next = Math.pow(2, x + 1)
        print(int(next))

# Driver Code
N = 3
findDistinctXOR(N)

# This code is contributed by Saurabh Jaiswal**
```

## ****C#****

```
**// C# code to implement above approach
using System;

class GFG{

static void findDistinctXOR(int n)
{

    // Corner case
    if (n == 1)
    {
        Console.WriteLine(1);
    }
    if (n == 2)
    {
        Console.WriteLine(2);
    }

    long x, next;
    x = (long)Math.Log(n, 2);

    // If n is power of two
    if ((n & (n - 1)) == 0)
    {
        next = (long)Math.Pow(2, x + 1);
        Console.WriteLine(next - 1);
    }
    else
    {
        next = (long)Math.Pow(2, x + 1);
        Console.WriteLine(next);
    }
}

// Driver Code
public static void Main()
{
    int N = 3;

    findDistinctXOR(N);
}
}

// This code is contributed by ukasp**
```

## ****java 描述语言****

```
**<script>
       // JavaScript code for the above approach
       function findDistinctXOR(n)
       {

           // Corner case
           if (n == 1) {
               document.write(1 + "<br>")
           }
           if (n == 2) {
               document.write(2 + "<br>")
           }
           let x, next;
           x = Math.floor(Math.log2(n));

           // if n is power of two
           if ((n & (n - 1)) == 0) {
               next = Math.pow(2, x + 1);
               document.write((next - 1) + "<br>")
           }
           else {
               next = Math.pow(2, x + 1);
               document.write(next + "<br>")
           }
       }

       // Driver Code
       let N = 3;
       findDistinctXOR(N);

 // This code is contributed by Potta Lokesh
   </script>**
```

******Output**

```
4
```**** 

******时间复杂度:**O(1)
T3】辅助空间: O(1)****