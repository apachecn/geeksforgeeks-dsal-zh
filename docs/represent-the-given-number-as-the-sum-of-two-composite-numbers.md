# 将给定的数表示为两个合成数的和

> 原文:[https://www . geeksforgeeks . org/将给定的数字表示为两个复合数字的总和/](https://www.geeksforgeeks.org/represent-the-given-number-as-the-sum-of-two-composite-numbers/)

给定一个整数 **N** ，任务是将 **N** 表示为两个复合整数之和。可能有多种方法，打印其中任何一种。如果无法将数字表示为两个合成数字的总和，则打印 **-1** 。
**举例:**

> **输入:**N = 13
> T3】输出: 4 9
> 4 + 9 = 13，4 和 9 都是复合的。
> **输入:** N = 18
> **输出:** 4 14

**趋近:**当 **N ≤ 11** 时，只有 **8** 和 **10** 是可以表示为两个复合整数之和的整数，即分别为 **4 + 4** 和 **4 + 6** 。
当 **N > 11** 时，则有两种情况:

1.  **当 N 为偶数时:** **N** 可以表示为**4+(N–4)**，因为两者都是复合的。
2.  **N 为奇数时:** **N** 可以表示为**9+(N–9)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find two composite
// numbers which when added
// give sum as n
void findNums(int n)
{

    // Only 8 and 10 can be represented
    // as the sum of two composite integers
    if (n <= 11) {
        if (n == 8)
            cout << "4 4";
        if (n == 10)
            cout << "4 6";
        else
            cout << "-1";
        return;
    }

    // If n is even
    if (n % 2 == 0)
        cout << "4 " << (n - 4);

    // If n is odd
    else
        cout << "9 " << (n - 9);
}

// Driver code
int main()
{
    int n = 13;

    findNums(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find two composite
// numbers which when added
// give sum as n
static void findNums(int n)
{

    // Only 8 and 10 can be represented
    // as the sum of two composite integers
    if (n <= 11)
    {
        if (n == 8)
            System.out.print("4 4");
        if (n == 10)
            System.out.print("4 6");
        else
            System.out.print("-1");
        return;
    }

    // If n is even
    if (n % 2 == 0)
        System.out.print("4 " + (n - 4));

    // If n is odd
    else
        System.out.print("9 " + (n - 9));
}

// Driver code
public static void main(String args[])
{
    int n = 13;

    findNums(n);
}
}

// This code is contributed by andrew1234
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find two composite
# numbers which when added
# give sum as n
def findNums(n):

    # Only 8 and 10 can be represented
    # as the sum of two composite integers
    if (n <= 11):
        if (n == 8):
            print("4 4", end = " ")
        if (n == 10):
            print("4 6", end = " ")
        else:
            print("-1", end = " ")

    # If n is even
    if (n % 2 == 0):
        print("4 ", (n - 4), end = " ")

    # If n is odd
    else:
        print("9 ", n - 9, end = " ")

# Driver code
n = 13

findNums(n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find two composite
    // numbers which when added
    // give sum as n
    static void findNums(int n)
    {

        // Only 8 and 10 can be represented
        // as the sum of two composite integers
        if (n <= 11)
        {
            if (n == 8)
                Console.Write("4 4");
            if (n == 10)
                Console.Write("4 6");
            else
                Console.Write("-1");
            return;
        }

        // If n is even
        if (n % 2 == 0)
            Console.Write("4 " + (n - 4));

        // If n is odd
        else
            Console.Write("9 " + (n - 9));
    }

    // Driver code
    public static void Main()
    {
        int n = 13;

        findNums(n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to find two composite
// numbers which when added
// give sum as n
function findNums(n)
{

    // Only 8 and 10 can be represented
    // as the sum of two composite integers
    if (n <= 11)
    {
        if (n == 8)
            document.write("4 4");
        if (n == 10)
            document.write("4 6");
        else
            document.write("-1");
        return;
    }

    // If n is even
    if (n % 2 == 0)
        document.write("4 " + (n - 4));

    // If n is odd
    else
        document.write("9 " + (n - 9));
}

// Driver code

var n = 13;

findNums(n);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
9 4
```