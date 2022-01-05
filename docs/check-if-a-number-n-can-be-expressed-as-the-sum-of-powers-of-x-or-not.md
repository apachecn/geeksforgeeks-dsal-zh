# 检查一个数 N 是否可以表示为 X 的幂之和

> 原文:[https://www . geesforgeks . org/check-if-a-number-n-可表示为-x-or-not 的幂之和/](https://www.geeksforgeeks.org/check-if-a-number-n-can-be-expressed-as-the-sum-of-powers-of-x-or-not/)

给定两个正数 **N** 和 **X** ，任务是检查给定的数字 **N** 是否可以表示为**X**T9】的不同[次幂之和。如果发现为真，则打印**“是”**，否则打印**“否”**。](https://www.geeksforgeeks.org/check-if-a-number-is-power-of-another-number/)

***例:***

> ***输入:** N = 10，X = 3*
> ***输出**:是*
> ***说明:***
> *给定值 N(= 10)可写成(1 + 9) = 3 <sup>0</sup> + 3 <sup>2</sup> 。因为 X(= 3)的所有幂都是不同的。因此，打印“是”。*
> 
> ***输入:** N= 12，X = 4*
> T5**输出:**否

**方法:**给定的问题可以通过检查[号 **N** 是否可以写成 base **X**](https://www.geeksforgeeks.org/given-number-n-decimal-base-find-number-digits-base-base-b/) 来解决。按照以下步骤解决问题:

*   [迭代一个循环](https://www.geeksforgeeks.org/range-based-loop-c/)直到 **N** 的值至少为**0**并执行以下步骤:
    *   当 **N** 除以 **X** 时，计算余数 **rem** 的值。
    *   如果 **rem** 的值至少为**2**，则打印**“否”**并返回。
    *   否则，将 **N** 的值更新为 **N / X** 。
*   完成上述步骤后，如果不存在任何终止，则打印**“是”**，因为 N 处的结果可以用 **X** 的不同幂表示。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// can be expressed as the sum of
// different powers of X or not
bool ToCheckPowerofX(int n, int x)
{
    // While n is a positive number
    while (n > 0) {

        // Find the remainder
        int rem = n % x;

        // If rem is at least 2, then
        // representation is impossible
        if (rem >= 2) {
            return false;
        }

        // Divide the value of N by x
        n = n / x;
    }

    return true;
}

// Driver Code
int main()
{
    int N = 10, X = 3;
    if (ToCheckPowerofX(N, X)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if the number N
// can be expressed as the sum of
// different powers of X or not
static boolean ToCheckPowerofX(int n, int x)
{

    // While n is a positive number
    while (n > 0)
    {

        // Find the remainder
        int rem = n % x;

        // If rem is at least 2, then
        // representation is impossible
        if (rem >= 2)
        {
            return false;
        }

        // Divide the value of N by x
        n = n / x;
    }
    return true;
}

// Driver Code
public static void main (String[] args)
{
    int N = 10, X = 3;
    if (ToCheckPowerofX(N, X))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the number N
# can be expressed as the sum of
# different powers of X or not
def ToCheckPowerofX(n, x):

    # While n is a positive number
    while (n > 0):

        # Find the remainder
        rem = n % x

        # If rem is at least 2, then
        # representation is impossible
        if (rem >= 2):
            return False

        # Divide the value of N by x
        n = n // x

    return True

# Driver Code
if __name__ == '__main__':

    N = 10
    X = 3

    if (ToCheckPowerofX(N, X)):
        print("Yes")
    else:
        print("No")

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if the number N
// can be expressed as the sum of
// different powers of X or not
static bool ToCheckPowerofX(int n, int x)
{

    // While n is a positive number
    while (n > 0)
    {

        // Find the remainder
        int rem = n % x;

        // If rem is at least 2, then
        // representation is impossible
        if (rem >= 2)
        {
            return false;
        }

        // Divide the value of N by x
        n = n / x;
    }
    return true;
}

// Driver code
public static void Main(String []args)
{
     int N = 10, X = 3;
    if (ToCheckPowerofX(N, X))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}
// This code is contributed by code_hunt,
```

## java 描述语言

```
<script>

// JavaScripts program for the above approach

// Function to check if the number N
// can be expressed as the sum of
// different powers of X or not
function ToCheckPowerofX(n, x)
{
    // While n is a positive number
    while (n > 0) {

        // Find the remainder
        var rem = n % x;

        // If rem is at least 2, then
        // representation is impossible
        if (rem >= 2) {
            return false;
        }

        // Divide the value of N by x
        n = n / x;
    }

    return true;
}

// Driver Code
    var N = 10, X = 3;
    if (ToCheckPowerofX(N, X)) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*