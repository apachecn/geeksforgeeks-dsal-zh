# 按位“或”和按位“与”之和等于 N 的非负对

> 原文:[https://www . geeksforgeeks . org/非负对加按位或与按位和等于 n/](https://www.geeksforgeeks.org/non-negative-pairs-with-sum-of-bitwise-or-and-bitwise-and-equal-to-n/)

给定一个整数 **N** ，任务是找到所有非负对 **(A，B)** ，使得 **A** 、 **B** 的[按位 OR 和按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 之和等于 **N** ，即 **(A | B) + (A & B) = N** 。

**示例:**

> **输入:** N = 5
> **输出:** (0，5)，(1，4)，(2，3)，(3，2)，(4，1)，(5，0)
> **说明:**满足必要条件的所有可能对:
> 
> 1.  (0 | 5) + (0 & 5) = 5 + 0 = 5
> 2.  (1 | 4) + (1 & 4) = 5 + 0 = 5
> 3.  (2 | 3) + (2 & 3) = 3 + 2 = 5
> 4.  (3 | 2) + (3 & 2) = 3 + 2 = 5
> 5.  (4 | 1) + (4 & 1) = 5 + 0 = 5
> 6.  (5 | 0) + (5 & 0) = 5 + 0 = 5
> 
> **输入:** N = 7
> **输出:** (0，7)，(1，6)，(2，5)，(3，4)，(4，3)，(5，2)，(6，1)，(7，0)
> **说明:**满足必要条件的所有可能对:
> 
> 1.  (0 | 7) + (0 & 7) = 7 + 0 =7
> 2.  (1 | 6) + (1 & 6) = 7 + 0 =7
> 3.  (2 | 5) + (2 & 5) = 7 + 0 =7
> 4.  (3 | 4) + (3 & 4) = 7 + 0 =7
> 5.  (4 | 3) + (4 & 3) = 7 + 0 =7
> 6.  (5 | 2) + (5 & 2) = 7 + 0 =7
> 7.  (6 | 1) + (6 & 1) = 7 + 0 = 7
> 8.  (7 | 0) + (7 & 0) = 7 + 0 = 7

**天真方法:**最简单的方法是迭代范围**【0，N】**并打印那些满足条件 **(A | B) + (A & B) = N** 的对 **(A，B)** 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，其思想是基于所有和等于 **N** 的非负对满足给定条件的观察。因此，使用变量 **i** 迭代范围**【0，N】**，并打印对 **i** 和**(N–I)**。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all pairs whose
// sum of Bitwise OR and AND is N
void findPairs(int N)
{
    // Iterate from i = 0 to N
    for (int i = 0; i <= N; i++) {

        // Print pairs (i, N - i)
        cout << "(" << i << ", "
             << N - i << "), ";
    }
}

// Driver Code
int main()
{
    int N = 5;
    findPairs(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to print all pairs whose
// sum of Bitwise OR and AND is N
static void findPairs(int N)
{

    // Iterate from i = 0 to N
    for(int i = 0; i <= N; i++)
    {

        // Print pairs (i, N - i)  
        System.out.print( "(" + i + ", " +
                          (N - i) + "), ");
   }
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    findPairs(N);
}
}

// This code is contributed by ajaykr00kj
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all pairs whose
# sum of Bitwise OR and AND is N
def findPairs(N):

     # Iterate from i = 0 to N
     for i in range(0, N + 1):

        # Print pairs (i, N - i)
        print("(", i, ",",
              N - i, "), ", end = "")

# Driver code
if __name__ == "__main__":

    N = 5

    findPairs(N)

# This code is contributed by ajaykr00kj
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print all pairs whose
// sum of Bitwise OR and AND is N
static void findPairs(int N)
{

    // Iterate from i = 0 to N
    for(int i = 0; i <= N; i++)
    {

        // Print pairs (i, N - i)  
        Console.Write( "(" + i + ", " +
                        (N - i) + "), ");
   }
}

// Driver code
public static void Main()
{
    int N = 5;

    findPairs(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to print all pairs whose
// sum of Bitwise OR and AND is N
function findPairs(N)
{

    // Iterate from i = 0 to N
    for(let i = 0; i <= N; i++)
    {

        // Print pairs (i, N - i) 
        document.write( "(" + i + ", " +
                          (N - i) + "), ");
   }
}

// Driver Code
  let N = 5;
  findPairs(N);

 // This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
(0, 5), (1, 4), (2, 3), (3, 2), (4, 1), (5, 0),
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)