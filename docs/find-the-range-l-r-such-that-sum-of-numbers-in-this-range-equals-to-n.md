# 找到范围【L，R】，使得该范围内的数字之和等于 N

> 原文:[https://www . geesforgeks . org/find-the-range-l-r-so-sum-of-numbers-in-to-n/](https://www.geeksforgeeks.org/find-the-range-l-r-such-that-sum-of-numbers-in-this-range-equals-to-n/)

给定一个整数 **N** (N ≠ 0)，任务是找到一个范围**【l，r】**(−10⁻⁸<l<r<10⁸)，使得该范围内所有整数之和等于 **N** 。

> L+(L+1)+…+(R1)+R = N

**示例:**

> **输入:** N = 3
> **输出:** -2 3
> **解释:**对于 L = -2 和 R = -3，和变为-2 + (-1) + 0 + 1 + 2 + 3 = 3
> 
> **输入:** N = -6
> **输出:** -6 5
> **说明:**这个范围的和[-6，5]是-6+(-5)+(-4)+(-3)+(-2)+(-1)+0+1+2+3+4+5 =-6

**天真方法:**对于 L 的每个值，试着找到一个满足 L + (L+1) +。。。+ (R-1) + R = N，使用嵌套循环。
**时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(1)

**有效方法:**由于 L 和 R 都是整数，也可以是负数，所以上述问题可以在 O(1)中有效地解决。考虑以下观察结果:

*   **对于 N 为正整数**我们可以考虑:

> [(N–1)]+[(N–2)]+。。。-1 + 0 + 1 + .。。+(n1)+N =
> -(N–1)+(N–1)–(N–2)+(N–2)+。。。+1–1+0+N = N
> 所以，**L =-(N–1)和 R = N**

*   同样**对于 N 为负数**，我们可以考虑:

> N + (N + 1) +。。。-1 + 0 + 1 + .。。+[-(N+2)]+[-(N+1)]=
> (N+1)–(N+1)+(N+2)–(N+2)+。。。-1 + 1 + 0 + N = N
> 所以 **L = N 和 R = -(N + 1)**

因此，单位时间复杂度的这个问题的解决方案是:

> 当 N 为正整数时，l =-(N–1)和 R = N。
> 
> L = N，R = -(N + 1)，当 N 为负整数时。

**注:**这是满足问题要求的最大可能范围(即 R–L 值最高)。

以下是该方法的实施情况:

## C++

```
// C++ code to implement above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find two integers
void Find_Two_Intergers(long long int N)
{
    // Variable to store value of L and R
    long long int L, R;

    // When N is positive
    if (N > 0) {
        L = -(N - 1);
        R = N;
    }

    // When N is negative
    else {
        L = N;
        R = -(N + 1);
    }
    cout << L << " " << R;
}

// Driver Code
int main()
{
    long long int N = 3;
    Find_Two_Intergers(N);
    return 0;
}
```

## C

```
// C code to implement above approach

#include <stdio.h>

// Function to find two integers
void Find_Two_Intergers(long long int N)
{
    // Variable to store L and R
    long long int L, R;

    // When N is positive
    if (N > 0) {
        L = -(N - 1);
        R = N;
    }

    // When N is negative
    else {
        L = N;
        R = -(N + 1);
    }
    printf("%lld %lld", L, R);
}

// Driver code
int main()
{
    long long int N = 3;
    Find_Two_Intergers(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

  // Function to find two integers
  static void Find_Two_Intergers(long  N)
  {

    // Variable to store value of L and R
    long  L, R;

    // When N is positive
    if (N > 0) {
      L = -(N - 1);
      R = N;
    }

    // When N is negative
    else {
      L = N;
      R = -(N + 1);
    }
    System.out.print( L + " " + R);
  }

  // Driver Code
  public static void main (String[] args) {

    long N = 3;
    Find_Two_Intergers(N);

  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code to implement above approach

# Function to find two integers
def Find_Two_Intergers(N):
    # variable to store L and R
    L = 0
    R = 0

    # When N is positive
    if N > 0:
        L = -(N-1)
        R = N

    # When N is negative
    else:
        L = N
        R = -(N+1)

    print(L, R)

# Driver code
N = 3
Find_Two_Intergers(N)
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

  // Function to find two integers
  static void Find_Two_Intergers(long  N)
  {

    // Variable to store value of L and R
    long  L, R;

    // When N is positive
    if (N > 0) {
      L = -(N - 1);
      R = N;
    }

    // When N is negative
    else {
      L = N;
      R = -(N + 1);
    }
    Console.Write( L + " " + R);
  }

  // Driver Code
  public static void Main (String[] args) {

    long N = 3;
    Find_Two_Intergers(N);

  }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript code to implement above approach

// Function to find two integers
function Find_Two_Intergers(N) {
    // Variable to store value of L and R
    let L, R;

    // When N is positive
    if (N > 0) {
        L = -(N - 1);
        R = N;
    }

    // When N is negative
    else {
        L = N;
        R = -(N + 1);
    }
    document.write(L + " " + R);
}

// Driver Code

let N = 3;
Find_Two_Intergers(N);

// This code is contributed by gfgking.
</script>
```

**Output**

```
-2 3
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)