# 将 N 个男孩和 M 个女孩放置在不同的排中，使得每排中放置的人数最大化

> 原文:[https://www . geesforgeks . org/place-n-boys-m-girls-in-different-row-使得每一行的人数最大化/](https://www.geeksforgeeks.org/place-n-boys-and-m-girls-in-different-rows-such-that-count-of-persons-placed-in-each-row-is-maximized/)

给定两个整数 **N** 和 **M** 代表男孩和女孩的数量，任务是将它们排列在相同大小的不同行的数量中，使得每行包含尽可能多的学生，并且每行应该包含男孩或女孩。
***注意:**没有一行可以同时包含男生和女生。*

***例:***

> ***输入:** N = 4，M = 2*
> **输出:** 2
> **说明:**
> 以下排列顺序满足给定条件:
> 1 <sup>st</sup> 行:B1，B2
> 2 <sup>nd</sup> 行:B3，B4
> 3 <sup>rd</sup> 行:G1，G2
> 清楚，每行
> 
> **输入:** N = 6，M = 6
> **输出:** 6
> **说明:**
> 以下排列顺序满足给定条件:
> 1 <sup>st</sup> 行:B1、B2、B3、B4、B5、B6
> 2 <sup>nd</sup> 行:G1、G2、G3、G4、G5、G6

**方法:**按照以下步骤解决问题

*   由于每行可以包含男孩或女孩，并且所有行的大小必须相同，因此最理想的排列方式是在每行中放置 **(N，M)** 数量的元素的[大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。
*   因此，打印 **GCD(N，M)** 作为所需答案。

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// GCD of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count maximum persons
// that can be placed in a row
int maximumRowValue(int n, int m) { return gcd(n, m); }

// Driver Code
int main()
{
    // Input
    int N = 4;
    int M = 2;

    // Function to count maximum
    // persons that can be placed in a row
    cout << maximumRowValue(N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to calculate
  // GCD of two numbers
  static int gcd(int a, int b)
  {
    if (b == 0)
      return a;

    return gcd(b, a % b);
  }

  // Function to count maximum persons
  // that can be placed in a row
  static int maximumRowValue(int n, int m) {
    return gcd(n, m);
  }

  // Driver Code
  public static void main(String args[])
  {
    // Input
    int N = 4;
    int M = 2;

    // Function to count maximum
    // persons that can be placed in a row
    System.out.print(maximumRowValue(N, M));
  }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to calculate
# GCD of two numbers
def gcd(a, b):
    if (b == 0):
        return a

    return gcd(b, a % b)

# Function to count maximum persons
# that can be placed in a row
def maximumRowValue(n, m):
    return gcd(n, m)

# Driver Code
if __name__ == '__main__':

    # Input
    N = 4
    M = 2

    # Function to count maximum
    # persons that can be placed in a row
    print (maximumRowValue(N, M))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Function to calculate
  // GCD of two numbers
  static int gcd(int a, int b)
  {
    if (b == 0)
      return a;

    return gcd(b, a % b);
  }

  // Function to count maximum persons
  // that can be placed in a row
  static int maximumRowValue(int n, int m) { return gcd(n, m); }

  // Driver Code
  public static void Main(String[] args)
  {

    // Input
    int N = 4;
    int M = 2;

    // Function to count maximum
    // persons that can be placed in a row
    Console.WriteLine(maximumRowValue(N, M));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// javascript Program to implement
// the above approach

    // Function to calculate
    // GCD of two numbers
    function gcd(a , b) {
        if (b == 0)
            return a;

        return gcd(b, a % b);
    }

    // Function to count maximum persons
    // that can be placed in a row
    function maximumRowValue(n , m) {
        return gcd(n, m);
    }

    // Driver Code

        // Input
        var N = 4;
        var M = 2;

        // Function to count maximum
        // persons that can be placed in a row
        document.write(maximumRowValue(N, M));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log N)*
***辅助** **空间:** O(1)*