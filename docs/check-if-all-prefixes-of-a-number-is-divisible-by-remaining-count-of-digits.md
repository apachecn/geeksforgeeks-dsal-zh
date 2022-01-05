# 检查一个数字的所有前缀是否能被剩余的位数整除

> 原文:[https://www . geesforgeks . org/check-如果数字的所有前缀都可以被剩余位数除尽/](https://www.geeksforgeeks.org/check-if-all-prefixes-of-a-number-is-divisible-by-remaining-count-of-digits/)

给定一个数字 **N，**任务是检查对于**I(***0<= I<= len***)**的每一个值，一个数字的第一个 **i** 位是否可以被**(len–I+1)**整除，其中 **len** 是 **N** 中的位数。如果发现是真的，则打印**“是”**。否则，打印**“否”。**

**示例:**

> **输入:** N = 52248。
> T3】输出:是
> T6】说明:
> 
> *   5 可以被 5 整除
> *   52 可以被 4 整除
> *   522 可以被 3 整除
> *   5224 可以被 2 整除
> *   52248 可以被 1 整除
> 
> **输入:**N = 59268
> T3】输出:否

**方法:**思想是遍历给定号码的所有[前缀](https://www.geeksforgeeks.org/tag/prefix/)，对于每个前缀，检查它是否满足条件。

按照以下步骤解决问题:

*   初始化一个变量，说 **i** 为 **1，**保持**的值(len–I+1**)。
*   当 **n** 大于 **0 时迭代。**
    *   如果 **N** 不能被 **i 整除，**则返回 **false。**
    *   否则将 **N** 除以 **10** ，将 **i** 的值增加 **1** 。
*   最后，返回 **true。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to check if all prefixes
// of a number is divisible by
// remaining count of digits or not
bool prefixDivisble(int n)
{
    int i = 1;

    while (n > 0) {

        // Traverse and check divisibility
        // for each updated number
        if (n % i != 0)
            return false;

        // Update the original number
        n = n / 10;

        i++;
    }

    return true;
}

// Driver Code
int main()
{
    // Given Input
    int n = 52248;

    // Function Call
    if (prefixDivisble(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program  for the above approach

import java.io.*;

class GFG{

// Function to check if all prefixes
// of a number is divisible by
// remaining count of digits or not
public static boolean prefixDivisble(int n)
{
    int i = 1;

    while (n > 0)
    {

        // Traverse and check divisibility
        // for each updated number
        if (n % i != 0)
            return false;

        // Update the original number
        n = n / 10;

        i++;
    }
    return true;
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    int n = 52248;

    // Function Call
    if (prefixDivisble(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if all prefixes of
# a number is divisible by remaining count
# of digits or not
def prefixDivisble(n):

    i = 1

    while n > 0:

        # Traverse and check divisibility
        # for each updated number
        if n % i != 0:
            return False

        # Update the original number
        n = n // 10
        i += 1

    return True

# Driver Code

# Given Input
n = 52248

# Function Call
if (prefixDivisble(n)):
   print("Yes")
else:
   print("No")

# This code is contributed by abhivick07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if all prefixes
// of a number is divisible by
// remaining count of digits or not
static bool prefixDivisble(int n)
{
    int i = 1;

    while (n > 0)
    {

        // Traverse and check divisibility
        // for each updated number
        if (n % i != 0)
            return false;

        // Update the original number
        n = n / 10;

        i++;
    }
    return true;
}

// Driver Code
public static void Main()
{

    // Given Input
    int n = 52248;

    // Function Call
    if (prefixDivisble(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if all prefixes
// of a number is divisible by
// remaining count of digits or not
function prefixDivisble(n)
{
    let i = 1;

    while (n > 0)
    {

        // Traverse and check divisibility
        // for each updated number
        if (n % i != 0)
            return false;

        // Update the original number
        n = parseInt(n / 10);

        i++;
    }
    return true;
}

// Driver Code

// Given Input
let n = 52248;

// Function Call
if (prefixDivisble(n) == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by lokeshpotta20.

</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(len)其中 len 为**n .**T5
*T8】辅助空间: O(1)**