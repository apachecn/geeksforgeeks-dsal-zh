# 统计奇数和偶数位置分别由偶数和素数组成的 N 位数

> 原文:[https://www . geeksforgeeks . org/count-n-digits-numbers-分别由奇数和偶数位置的偶数和素数组成/](https://www.geeksforgeeks.org/count-n-digits-numbers-made-up-of-even-and-prime-digits-at-odd-and-even-positions-respectively/)

给定一个正整数 **N** ，任务是找出奇数索引处为偶数的 **N 位**和偶数索引处为素数的[位](https://www.geeksforgeeks.org/tag/prime-number/)的整数个数。

**示例:**

> **输入:** N = 2
> **输出:** 20
> **解释:**
> 以下是满足给定标准{20，22，24，26，28，30，32，34，36，38，50，52，54，56，58，70，72，74，76，78}的可能的 2 位数。因此，这个数字的计数是 20。
> 
> **输入:**N = 5
> T3】输出: 1600

**方法:**通过观察**偶数位置**作为**【2，3，5，7】**和 **5** 选择**奇数位置**作为**【0，2，4，6，8】**只有 **4** 选择这一事实，可以使用 [**排列组合**](https://www.geeksforgeeks.org/permutation-and-combination/) 的概念来解决给定的问题。因此，满足给定标准的 N 位数的计数由下式给出:

> 总计数= 4 <sup>P</sup> 5 <sup>Q</sup> ，其中 P 和 Q 分别为偶数和奇数位的个数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approache
#include<bits/stdc++.h>
using namespace std;

int m = 1000000007;

// Function to find the value of x ^ y
int power(int x, int y)
{

    // Stores the value of x ^ y
    int res = 1;

    // Iterate until y is positive
    while (y > 0)
    {

        // If y is odd
        if ((y & 1) != 0)
            res = (res * x) % m;

        // Divide y by 2
        y = y >> 1;

        x = (x * x) % m;
    }

    // Return the value of x ^ y
    return res;
}

// Function to find the number of N-digit
// integers satisfying the given criteria
int countNDigitNumber(int N)
{

    // Count of even positions
    int ne = N / 2 + N % 2;

    // Count of odd positions
    int no = floor(N / 2);

    // Return the resultant count
    return power(4, ne) * power(5, no);
}

// Driver Code
int main()
{
    int N = 5;
    cout << countNDigitNumber(N) % m << endl;
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

static int m = 1000000007;

// Function to find the value of x ^ y
static int power(int x, int y)
{

    // Stores the value of x ^ y
    int res = 1;

    // Iterate until y is positive
    while (y > 0)
    {

        // If y is odd
        if ((y & 1) != 0)
            res = (res * x) % m;

        // Divide y by 2
        y = y >> 1;

        x = (x * x) % m;
    }

    // Return the value of x ^ y
    return res;
}

// Function to find the number of N-digit
// integers satisfying the given criteria
static int countNDigitNumber(int N)
{

    // Count of even positions
    int ne = N / 2 + N % 2;

    // Count of odd positions
    int no = (int)Math.floor(N / 2);

    // Return the resultant count
    return power(4, ne) * power(5, no);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    System.out.println(countNDigitNumber(N) % m);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

import math
m = 10**9 + 7

# Function to find the value of x ^ y
def power(x, y):

    # Stores the value of x ^ y
    res = 1

    # Iterate until y is positive
    while y > 0:

        # If y is odd
        if (y & 1) != 0:
            res = (res * x) % m

        # Divide y by 2
        y = y >> 1

        x = (x * x) % m

    # Return the value of x ^ y
    return res

# Function to find the number of N-digit
# integers satisfying the given criteria
def countNDigitNumber(n: int) -> None:

    # Count of even positions
    ne = N // 2 + N % 2

    # Count of odd positions
    no = N // 2

    # Return the resultant count
    return power(4, ne) * power(5, no)

# Driver Code
if __name__ == '__main__':

    N = 5
    print(countNDigitNumber(N) % m)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int m = 1000000007;

// Function to find the value of x ^ y
static int power(int x, int y)
{

    // Stores the value of x ^ y
    int res = 1;

    // Iterate until y is positive
    while (y > 0)
    {

        // If y is odd
        if ((y & 1) != 0)
            res = (res * x) % m;

        // Divide y by 2
        y = y >> 1;

        x = (x * x) % m;
    }

    // Return the value of x ^ y
    return res;
}

// Function to find the number of N-digit
// integers satisfying the given criteria
static int countNDigitNumber(int N)
{

    // Count of even positions
    int ne = N / 2 + N % 2;

    // Count of odd positions
    int no = (int)Math.Floor((double)N / 2);

    // Return the resultant count
    return power(4, ne) * power(5, no);
}

// Driver Code
public static void Main()
{
    int N = 5;
    Console.Write(countNDigitNumber(N) % m);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
   <script>

        // JavaScript program for the above approache

        var m = 10 ** 9 + 7

        // Function to find the value of x ^ y
        function power(x, y) {

            // Stores the value of x ^ y
            var res = 1

            // Iterate until y is positive
            while (y > 0) {

                // If y is odd
                if ((y & 1) != 0)
                    res = (res * x) % m

                // Divide y by 2
                y = y >> 1

                x = (x * x) % m
            }
            // Return the value of x ^ y
            return res
        }
        // Function to find the number of N-digit
        // integers satisfying the given criteria
        function countNDigitNumber(N) {

            // Count of even positions
            var ne = Math.floor(N / 2) + N % 2

            // Count of odd positions
            var no = Math.floor(N / 2)

            // Return the resultant count
            return power(4, ne) * power(5, no)
        }
        // Driver Code

        let N = 5
        document.write(countNDigitNumber(N) % m);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
1600
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*