# 求数列 0、1、1、2、5、29、841 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n 系列术语-0-1-1-2-5-29-841/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-0-1-1-2-5-29-841/)

给定一个正整数 **N** ，任务是找到系列 **0，1，1，2，5，29，841** 中的 **N** 项…

**示例:**

> **输入:** N = 6
> **输出:** 29
> **说明:**给定数列的第 6 项是 29。
> 
> **输入:**N = 1
> T3】输出: 1
> 
> **输入:**N = 8
> T3】输出: 750797

**方法:**给定的问题是一个基本的[数学基础的](https://www.geeksforgeeks.org/mathematical-algorithms/)问题，其中 A<sub>I</sub>= A<sub>I-1</sub><sup>2</sup>+A<sub>I-2</sub><sup>2</sup>。因此，创建变量 **a = 0** 和 **b = 1** 。使用范围**【2，N】**中的变量 **i** 进行迭代，对于每个 **i** ，计算**I<sup>th</sup>T29】项，并将 **a** 和 **b** 的值更新为**I–1<sup>th</sup>T37】和**I–2<sup>th</sup>******

下面是上述方法的实现:

## C++

```
// C++ program for the above aproach
#include <bits/stdc++.h>
using namespace std;

// Function to find N-th term
// of the given series
int getNthTerm(int N)
{
    if (N < 3)
        return N - 1;

    // Initialize Variables repre-
    // senting 1st and 2nd term
    long int a = 0, b = 1;

    // Loop to iterate through the
    // range [3, N] using variable i
    for (int i = 3; i <= N; i++) {

        // pow((i - 2)th term, 2) +
        // pow((i - 1)th term, 2)
        long int c = a * a + b * b;

        // Update a and b
        a = b;
        b = c;
    }

    // Return Answer
    return b;
}

// Driver Code
int main()
{
    int N = 8;
    cout << getNthTerm(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above aproach
import java.util.*;
class GFG{

  // Function to find N-th term
  // of the given series
  static int getNthTerm(int N)
  {
    if (N < 3)
      return N - 1;

    // Initialize Variables repre-
    // senting 1st and 2nd term
    int a = 0, b = 1;

    // Loop to iterate through the
    // range [3, N] using variable i
    for (int i = 3; i <= N; i++) {

      // Math.pow((i - 2)th term, 2) +
      // Math.pow((i - 1)th term, 2)
      int c = a * a + b * b;

      // Update a and b
      a = b;
      b = c;
    }

    // Return Answer
    return b;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 8;
    System.out.print(getNthTerm(N));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find N-th term
# of the given series
def getNthTerm(N):
    if (N < 3):
        return N - 1

    # Initialize Variables repre-
    # senting 1st and 2nd term
    a = 0
    b = 1

    # Loop to iterate through the
    # range [3, N] using variable i
    for i in range(3, N + 1):

        # pow((i - 2)th term, 2) +
        # pow((i - 1)th term, 2)
        c = a * a + b * b

        # Update a and b
        a = b
        b = c

    # Return Answer
    return b

# Driver Code
N = 8
print(getNthTerm(N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above aproach
using System;
class GFG
{

// Function to find N-th term
// of the given series
static int getNthTerm(int N)
{
    if (N < 3)
        return N - 1;

    // Initialize Variables repre-
    // senting 1st and 2nd term
    long a = 0, b = 1;

    // Loop to iterate through the
    // range [3, N] using variable i
    for (int i = 3; i <= N; i++) {

        // pow((i - 2)th term, 2) +
        // pow((i - 1)th term, 2)
        long c = a * a + b * b;

        // Update a and b
        a = b;
        b = c;
    }

    // Return Answer
    return (int)b;
}

// Driver Code
public static void Main()
{
    int N = 8;
    Console.Write(getNthTerm(N));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
  // JavaScript code for the above approach

  // Function to find N-th term
  // of the given series
  function getNthTerm(N) {
    if (N < 3)
      return N - 1;

    // Initialize Variables repre-
    // senting 1st and 2nd term
    let a = 0, b = 1;

    // Loop to iterate through the
    // range [3, N] using variable i
    for (let i = 3; i <= N; i++) {

      // pow((i - 2)th term, 2) +
      // pow((i - 1)th term, 2)
      let c = a * a + b * b;

      // Update a and b
      a = b;
      b = c;
    }

    // Return Answer
    return b;
  }

  // Driver Code

  let N = 8;
  document.write(getNthTerm(N));

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
750797
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)