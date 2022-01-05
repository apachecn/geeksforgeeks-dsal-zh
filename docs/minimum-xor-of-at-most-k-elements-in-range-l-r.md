# 范围【L，R】

内最多 K 个元素的最小异或

> 原文:[https://www . geeksforgeeks . org/最小-最多 k 个范围内元素的异或-l-r/](https://www.geeksforgeeks.org/minimum-xor-of-at-most-k-elements-in-range-l-r/)

给定三个整数 **L** 、 **R** 和 **K** ，任务是求**【L，R】**之间最多 K 个**的最小[位异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)。**

**示例:**

> **输入:** L = 1，R = 10，K = 3
> **输出:** 0
> **说明:**
> 在[1，10]范围内选择元素 4，5，1，所选元素的按位异或为 0，为最小值。
> 
> **输入:** L = 32，R = 33，K = 2
> **输出:** 1
> **说明:**
> 在[32，33]范围内选择元素 32，33，所选元素的按位异或为 1，最小。

**方法:**一个帮助我们解决问题的观察是两个数 **X** 和 **(X+1)** 的**逐位异或**如果 **X** 是偶数，则为 **1** 。因此，如果第一个数字为偶数，四个连续数字的**按位异或**将为 **0** 。

按照以下步骤解决问题:

*   如果 **K** 的值大于 **4** ，那么答案总是 **0。**(这是因为四个数字 **X、(X+1)、(X+2)、**和 **(X+3)** 总是可以在 **5** 的范围内找到，其中 **X** 是偶数。)
*   如果 **K** 的值为 **2** ，调用以 **L、R** 、**T9、 **K** 为输入参数的函数 **func2()** ，并执行以下操作:**
    *   如果 **(R-L)** 的值大于或等于 **2** ，即范围内至少有 **3** 个数字，则返回 **1** 。(这是因为两个数字 **X** 和 **X+1** 总是可以在 **3** 的范围内找到，其中 **X** 是偶数。)
    *   否则，返回 **L** 和**的最小值(L^R).**
*   如果 **K** 的值为 **3** ，则调用以 **L、****【R】**、和 **K** 为输入参数的函数 **func3()** ，并执行以下操作:
    *   如果 **(R^L)** 位于 **L** 和 **R** 之间，返回 **0** 。(这是因为 **(R^L)^L^R=0)** )
    *   否则，返回**函数 2(L，R，** **K)**
*   如果 **K** 的值为 **4** ，调用以 **L、R** 、**T9、 **K** 为输入参数的函数 **func4()** ，并执行以下操作:**
    *   如果 **(R-L)** 大于等于 **4** ，即范围内至少有 **5** 个数字，则返回 **0。**(这是因为四个数字 **X、(X+1)、(X+2)** 、**和(X+3)** 总是可以在 **5** 的范围内找到，其中 **X** 是偶数。)
    *   否则，返回[L，**和 **func3(L，R，K)** 范围内四个数的最小**异或。****
*   **否则，返回 **L.****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function for K=2
int func2(int L, int R, int K)
{
    if (R - L >= 2)
        return 1;
    return min(L, L ^ R);
}
// Function for K=2
int func3(int L, int R, int K)
{
    if ((R ^ L) > L && (R ^ L) < R)
        return 0;
    return func2(L, R, K);
}
// Function for K=2
int func4(int L, int R, int K)
{
    if (R - L >= 4)
        return 0;
    int minval = L ^ (L + 1) ^ (L + 2) ^ (L + 3);
    return min(minval, func3(L, R, K));
}
// Function to calculate the minimum XOR of at most K
// elements in [L, R]
int minimumXor(int L, int R, int K)
{
    if (K > 4)
        return 0;
    else if (K == 4)
        return func4(L, R, K);
    else if (K == 3)
        return func3(L, R, K);
    else if (K == 2)
        return func2(L, R, K);
    else
        return L;
}
// Driver code
int main()
{
    // Input
    int L = 1, R = 3, K = 3;
    // Function call
    cout << minimumXor(L, R, K) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG
{

// Function for K=2
static int func2(int L, int R, int K)
{
    if (R - L >= 2)
        return 1;
    return Math.min(L, L ^ R);
}

// Function for K=2
static int func3(int L, int R, int K)
{
    if ((R ^ L) > L && (R ^ L) < R)
        return 0;
    return func2(L, R, K);
}

// Function for K=2
static int func4(int L, int R, int K)
{
    if (R - L >= 4)
        return 0;
    int minval = L ^ (L + 1) ^ (L + 2) ^ (L + 3);
    return Math.min(minval, func3(L, R, K));
}
// Function to calculate the minimum XOR of at most K
// elements in [L, R]
static int minimumXor(int L, int R, int K)
{
    if (K > 4)
        return 0;
    else if (K == 4)
        return func4(L, R, K);
    else if (K == 3)
        return func3(L, R, K);
    else if (K == 2)
        return func2(L, R, K);
    else
        return L;
}

  // Driver code
  public static void main(String[] args)
  {
      // Input
    int L = 1, R = 3, K = 3;

    // Function call
    System.out.println( minimumXor(L, R, K));
  }
}

// This code is contributed by sanjoy_62.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function for K=2
def func2(L, R, K):
    if (R - L >= 2):
        return 1
    return min(L, L ^ R)

  # Function for K=2
def func3(L, R, K):
    if ((R ^ L) > L and (R ^ L) < R):
        return 0
    return func2(L, R, K)

# Function for K=2
def func4(L, R, K):
    if (R - L >= 4):
        return 0
    minval = L ^ (L + 1) ^ (L + 2) ^ (L + 3)
    return min(minval, func3(L, R, K))

# Function to calculate the minimum XOR of at most K
# elements in [L, R]
def minimumXor(L, R, K):
    if (K > 4):
        return 0
    elif (K == 4):
        return func4(L, R, K)
    elif (K == 3):
        return func3(L, R, K)
    elif (K == 2):
        return func2(L, R, K)
    else:
        return L

# Driver code
if __name__ == '__main__':

    # Input
    L, R, K = 1, 3, 3

    # Function call
    print (minimumXor(L, R, K))

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

// Function for K=2
static int func2(int L, int R, int K)
{
    if (R - L >= 2)
        return 1;
    return Math.Min(L, L ^ R);
}

// Function for K=2
static int func3(int L, int R, int K)
{
    if ((R ^ L) > L && (R ^ L) < R)
        return 0;
    return func2(L, R, K);
}

// Function for K=2
static int func4(int L, int R, int K)
{
    if (R - L >= 4)
        return 0;
    int minval = L ^ (L + 1) ^ (L + 2) ^ (L + 3);
    return Math.Min(minval, func3(L, R, K));
}
// Function to calculate the minimum XOR of at most K
// elements in [L, R]
static int minimumXor(int L, int R, int K)
{
    if (K > 4)
        return 0;
    else if (K == 4)
        return func4(L, R, K);
    else if (K == 3)
        return func3(L, R, K);
    else if (K == 2)
        return func2(L, R, K);
    else
        return L;
}

// Driver code
static void Main()
{
    // Input
    int L = 1, R = 3, K = 3;

    // Function call
    Console.Write( minimumXor(L, R, K));

}
}

// This code is contributed by code_hunt.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function for K=2
function func2(L, R, K)
{
    if (R - L >= 2)
        return 1;

    return Mat.min(L, L ^ R);
}

// Function for K=2
function func3(L, R, K)
{
    if ((R ^ L) > L && (R ^ L) < R)
        return 0;

    return func2(L, R, K);
}

// Function for K=2
function func4(L, R, K)
{
    if (R - L >= 4)
        return 0;

    var minval = L ^ (L + 1) ^
                (L + 2) ^ (L + 3);
    return Math.min(minval, func3(L, R, K));
}

// Function to calculate the minimum XOR
// of at most K elements in [L, R]
function minimumXor(L, R, K)
{
    if (K > 4)
        return 0;
    else if (K == 4)
        return func4(L, R, K);
    else if (K == 3)
        return func3(L, R, K);
    else if (K == 2)
        return func2(L, R, K);
    else
        return L;
}

// Driver code

// Input
var L = 1, R = 3, K = 3;

// Function call
document.write(minimumXor(L, R, K));

// This code is contributed by SURENDRA_GANGWAR

</script>
```

****Output**

```
0
```** 

*****时间复杂度:**O(1)*
T5**辅助空间:** O(1)**