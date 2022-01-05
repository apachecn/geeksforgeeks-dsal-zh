# 求 K 的最小值，使得[N，N-K]范围内数字的位“与”为 0

> 原文:[https://www . geesforgeks . org/find-k 的最小值，即范围内数字的按位和-n-n-k-is-0/](https://www.geeksforgeeks.org/find-smallest-value-of-k-such-that-bitwise-and-of-numbers-in-range-n-n-k-is-0/)

给定一个整数 **N** ，任务是找到最小的数 **K** ，使得范围【N，N-K】内所有数的位“与”为 0，即**N&(N–1)&(N–2)&……(N–K)= 0**。

**示例:**

> **输入:** N = 17
> 
> **输出:** 2
> 
> **说明:**
> 
> 17&16 = 16
> 
> 16&15 = 0
> 
> 因为，我们需要找到最小的 K，所以我们就此打住。
> 
> k = N–15 = 17–15 = 2
> 
> **输入:** N = 4
> 
> **输出:** 1
> 
> **说明:**
> 
> 4&3 = 0
> 
> 因为，我们需要找到最小的 k，所以我们就此打住。

**天真法:**解决问题最简单的方法就是从给定的数开始，用比当前数少一个数的[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) ，直到累计[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 不等于 **0** 。按照以下步骤解决此问题:

*   声明一个变量 **cummAnd** ，它存储交换的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，并用 **n** 初始化它。
*   声明一个变量 **i** 和**T3【用**n–1 初始化它。****
*   运行一个循环，同时**命令**不等于 **0:**
    *   **系泊器=系泊器&。**
    *   将 **i** 减少 **1。**
*   最后，打印**n–I .**

下面是以下方法的实现:

## C++

```
// C++ program to find smallest value of K
// such that bitwise AND of numbers
// in range [N, N-K] is 0

#include <iostream>
using namespace std;

// Function is to find the largest no which gives the
// sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
int findSmallestNumK(int n)
{
    int cummAnd = n;

    int i = n - 1;
    // Since, we need the largest no,
    // we start from n itself, till 0
    while (cummAnd != 0) {

        cummAnd = cummAnd & i;
        if (cummAnd == 0) {
            return i;
        }

        i--;
    }

    return -1;
}

// Driver Code
int main()
{

    int N = 17;
    int lastNum = findSmallestNumK(N);
    int K = lastNum == -1 ? lastNum : N - lastNum;
    cout << K << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function is to find the largest no which gives the
    // sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
    public static int findSmallestNumK(int n)
    {
        int cummAnd = n;
        int i = n - 1;

        // Since, we need the largest no,
        // we start from n itself, till 0
        while (cummAnd != 0) {

            cummAnd = cummAnd & i;
            if (cummAnd == 0) {
                return i;
            }

            i--;
        }

        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 17;
        int lastNum = findSmallestNumK(N);
        int K = lastNum == -1 ? lastNum : N - lastNum;
        System.out.println(K);

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program to find smallest value of K
# such that bitwise AND of numbers
# in range [N, N-K] is 0

# Function is to find the largest no which gives the
# sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
def findSmallestNumK(n):

    cummAnd = n
    i = n - 1

    # Since, we need the largest no,
    # we start from n itself, till 0
    while (cummAnd != 0):
        cummAnd = cummAnd & i

        if (cummAnd == 0):
            return i

        i -= 1

    return -1

# Driver Code
if __name__ == '__main__':

    N = 17
    lastNum = findSmallestNumK(N);
    K = lastNum if lastNum == -1 else N - lastNum

    print(K)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function is to find the largest no which gives the
// sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
public static int findSmallestNumK(int n)
{
    int cummAnd = n;
    int i = n - 1;

    // Since, we need the largest no,
    // we start from n itself, till 0
    while (cummAnd != 0)
    {
        cummAnd = cummAnd & i;
        if (cummAnd == 0)
        {
            return i;
        }
        i--;
    }
    return -1;
}

// Driver code
static void Main()
{
    int N = 17;
    int lastNum = findSmallestNumK(N);
    int K = lastNum == -1 ? lastNum : N - lastNum;

    Console.WriteLine(K);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function is to find the largest no which gives the
       // sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
       function findSmallestNumK(n)
       {
           let cummAnd = n;

           let i = n - 1;

           // Since, we need the largest no,
           // we start from n itself, till 0
           while (cummAnd != 0) {

               cummAnd = cummAnd & i;
               if (cummAnd == 0) {
                   return i;
               }

               i--;
           }

           return -1;
       }

       // Driver Code
       let N = 17;
       let lastNum = findSmallestNumK(N);
       let K = lastNum == -1 ? lastNum : N - lastNum;
       document.write(K + "<br>");

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
2
```

***时间复杂度** : O(N)*

***辅助空间** : O(1)*

**有效方法:**这个问题可以通过使用[按位“与”运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的属性来解决，即如果两个位都被设置，那么只有结果是非零的。所以我们要找到 **2** 的最大功率，小于等于 **N** (假设 **X** )。按照以下步骤解决此问题:

*   [log2(n)](https://www.geeksforgeeks.org/log2-function-in-c-with-examples/) 功能给出 **2** 的功率，等于 **n** 。
*   因为，它的返回类型是双重的。所以我们使用 [floor](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 函数获取 **2** 的最大功率，小于等于 **n** 并存储到 **X.**
*   **X =(1<<X)–1。**
*   最后，打印**N–x .**

下面是以下方法的实现:

## C++

```
// C++ program to find smallest value of K
// such that bitwise AND of numbers
// in range [N, N-K] is 0

#include <bits/stdc++.h>
using namespace std;

// Function is to find the largest no which gives the
// sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
int findSmallestNumK(int n)
{

    // find largest power of 2
    // less than or equal to n
    int larPowOfTwo = floor(log2(n));

    larPowOfTwo = 1 << larPowOfTwo;

    return larPowOfTwo - 1;
}

// Driver Code
int main()
{

    int N = 17;
    int lastNum = findSmallestNumK(N);
    int K = lastNum == -1 ? lastNum : N - lastNum;
    cout << K << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest value of K
// such that bitwise AND of numbers
// in range [N, N-K] is 0
import java.io.*;

class GFG {

    // Function is to find the largest no which gives the
    // sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
    static int findSmallestNumK(int n)
    {

        // find largest power of 2
        // less than or equal to n
        int larPowOfTwo
            = (int)Math.floor(Math.log(n) / Math.log(2));

        larPowOfTwo = 1 << larPowOfTwo;

        return larPowOfTwo - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 17;
        int lastNum = findSmallestNumK(N);
        int K = lastNum == -1 ? lastNum : N - lastNum;
        System.out.println(K);
    }
}

// This code is contributed by rishavmahato348.
```

## 蟒蛇 3

```
# Python program to find smallest value of K
# such that bitwise AND of numbers
# in range [N, N-K] is 0
# Function is to find the largest no which gives the
# sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
import math

def findSmallestNumK( n):

    # find largest power of 2
    # less than or equal to n
    larPowOfTwo = math.floor(math.log2(n))

    larPowOfTwo = 1 << larPowOfTwo

    return larPowOfTwo - 1

# Driver Code
N = 17
lastNum = findSmallestNumK(N)
K = lastNum if (lastNum == -1 ) else N - lastNum
print(K)

# this code is contributed by shivanisinghss2110
```

## C#

```
// C# program to find smallest value of K
// such that bitwise AND of numbers
// in range [N, N-K] is 0
using System;

class GFG{

// Function is to find the largest no which gives the
// sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
static int findSmallestNumK(int n)
{

    // Find largest power of 2
    // less than or equal to n
    int larPowOfTwo = (int)Math.Floor(Math.Log(n) /
                                      Math.Log(2));

    larPowOfTwo = 1 << larPowOfTwo;

    return larPowOfTwo - 1;
}

// Driver Code
public static void Main()
{
    int N = 17;
    int lastNum = findSmallestNumK(N);
    int K = lastNum == -1 ? lastNum : N - lastNum;

    Console.Write(K);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// JavaScript program to find smallest value of K
// such that bitwise AND of numbers
// in range [N, N-K] is 0
// Function is to find the largest no which gives the
// sequence n & (n - 1) & (n - 2)&.....&(n - k) = 0.
function findSmallestNumK(n)
    {

        // find largest power of 2
        // less than or equal to n
        var larPowOfTwo
            = Math.floor(Math.log(n) / Math.log(2));

        larPowOfTwo = 1 << larPowOfTwo;

        return larPowOfTwo - 1;
    }

// Driver Code
    var N = 17;
    var lastNum = findSmallestNumK(N);
    var K = lastNum == -1 ? lastNum : N - lastNum;
    document.write(K);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
2
```

***时间复杂度:** O(对数 N)*

***空间复杂度:** O(1)*