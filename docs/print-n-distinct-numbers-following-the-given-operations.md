# 按照给定的操作打印 N 个不同的数字

> 原文:[https://www . geeksforgeeks . org/print-n-distinct-numbers-follow-the-then-operations/](https://www.geeksforgeeks.org/print-n-distinct-numbers-following-the-given-operations/)

给定一个始终为偶数的**整数 N** ，我们的任务是按照给定的条件打印 **N** 个不同的数字:

*   前半部分数字是偶数，而另一半数字是奇数
*   前半数的元素和后半数的元素和应该相等

如果上述条件满足，则打印数组，否则输出“-1”。
**例:**

> **输入:** N = 4
> **输出:** 2 4 1 5
> **说明:**
> 给定数字 4 我们需要打印 4 个数字。前半部分= 2，4，它们的和是 6，另一半= 1，5，它们的和也是 6。
> **输入:** N = 22
> **输出:** -1
> **说明:**
> 无法打印所需数组。

**方法:**
要解决上面提到的问题，我们必须观察到**整数 N 必须是 4 的倍数**。

*   我们知道前 N/2 个偶数的**和将是偶数**，所以如果其他 N/2 个整数的和也是偶数，那么 N/2 一定是偶数，因为奇数个奇数的**和总是奇数。**
*   如果 N/2 是偶数，那么 N 是 4 的倍数，所以如果 N 不能被 4 整除，那么答案是“-1”，否则，会有一个可能的数组。
*   为了打印数组，我们将考虑两个部分，即第一个部分是 N/2 个元素，是 2 的倍数，另一半是 2–1 的倍数。对于数组中的最后一个元素，我们将通过应用直接公式 N+N/2–1 来计算整数，因为我们应该使两半的和相等。

以下是上述方法的实现:

## C++

```
// C++ implementation to Print N distinct numbers
#include <bits/stdc++.h>
using namespace std;

// Function to print the required array
bool printArr(int n)
{

    // Check if number is a multiple of 4
    if (n % 4 == 0) {
        // Printing Left Half of the array
        for (int i = 1; i <= n / 2; i++)
            cout << i * 2 << ' ';

        // Printing Right Half of the array
        for (int i = 1; i < n / 2; i++)
            cout << i * 2 - 1 << ' ';
        cout << n + n / 2 - 1 << '\n';
    }

    else
        cout << "-1";
}

// Driver code
int main()
{
    int n = 22;

    printArr(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print N distinct numbers
import java.util.*;

class GFG{

// Function to print the required array
static void printArr(int n)
{

    // Check if number is a multiple of 4
    if(n % 4 == 0)
    {
       // Printing left half of the array
       for(int i = 1; i <= n / 2; i++)
           System.out.print(i * 2 + " ");

       // Printing Right Half of the array
       for(int i = 1; i < n / 2; i++)
           System.out.print(i * 2 - 1 + " ");

       System.out.println(n + n / 2 - 1);
    }
    else
        System.out.print("-1");
}

// Driver code
public static void main(String[] args)
{
    int n = 22;
    printArr(n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to print
# N distinct numbers

# Function to print the required array
def printArr(n):

    # Check if number is a multiple of 4
    if (n % 4 == 0):

        # Printing Left Half of the array
        for i in range(1, (n / 2) + 1):
            print (i * 2, end = " ")

        # Printing Right Half of the array
        for i in range(1, n / 2):
            print (i * 2 - 1, end = " ")

        print (n + n / 2 - 1, end = "\n")

    else:
        print ("-1")

# Driver code
n = 22
printArr(n)

# This code is contributed by PratikBasu
```

## C#

```
// C# implementation to print N distinct numbers
using System;

public class GFG{

// Function to print the required array
static void printArr(int n)
{

    // Check if number is a multiple of 4
    if(n % 4 == 0)
    {

    // Printing left half of the array
    for(int i = 1; i <= n / 2; i++)
        Console.Write(i * 2 + " ");

    // Printing Right Half of the array
    for(int i = 1; i < n / 2; i++)
        Console.Write(i * 2 - 1 + " ");

    Console.WriteLine(n + n / 2 - 1);
    }

    else
        Console.Write("-1");
}

// Driver code
public static void Main(String[] args)
{
    int n = 22;
    printArr(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to Print N distinct numbers

// Function to print the required array
function printArr(n)
{

    // Check if number is a multiple of 4
    if (n % 4 == 0) {
        // Printing Left Half of the array
        for (var i = 1; i <= n / 2; i++)
            document.write( i * 2 + ' ');

        // Printing Right Half of the array
        for (var i = 1; i < n / 2; i++)
            document.write( i * 2 - 1 + ' ');
        document.write( n + n / 2 - 1 + '<br>');
    }

    else
        document.write( "-1");
}

// Driver code
var n = 22;
printArr(n);

</script>
```

**Output:** 

```
-1
```

**时间复杂度:** O(N)

**辅助空间:** O(1)