# 检查前 N 个自然数的连接是否能被 3 整除

> 原文:[https://www . geesforgeks . org/check-first-n-自然数的连接是否可被 3 整除/](https://www.geeksforgeeks.org/check-if-the-concatenation-of-first-n-natural-numbers-is-divisible-by-3/)

给定一个整数 **N** ，任务是检查第一个 **N** 自然[数的连接是否可以被*除以*再除以 3](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/) 。可分则打印 ***是*** ，不可分则打印 ***否*** 。

**示例**:

> **输入** : N = 3
> **输出:**是
> **说明:**
> 连接数= 123
> 由于能被 3 整除，输出为是
> **输入** : N = 7
> **输出:**否
> **说明:**连接数= 1234567
> 由于不能被 3 整除，输出为

**天真法** :
最简单的方法是将第一个 **N 个**自然数串联起来，计算结果数的位数之和，检查是否能被 3 整除。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*
**高效进场:**
为了优化上述进场，我们可以观察到一个模式。对于下列系列 *1、4、7、10、13、16、19* 、*等，第一个 **N** 自然数的串联不能被 3 整除。*该系列的***N<sup>th</sup>*****术语**由公式 **3×n +1** ***给出。*** 因此，如果**(N–1)**不能被 **3** 整除，那么结果数可以被 3 整除，所以打印*是*。否则，打印*号*
以下是执行上述办法:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function that returns True if
// concatenation of first N natural
// numbers is divisible by 3
bool isDivisible(int N)
{
    // Check using the formula
    return (N - 1) % 3 != 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 6;

    // Function Call
    if (isDivisible(N))
        cout << ("Yes");

    else
        cout << ("No");

    return 0;
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that returns True if
// concatenation of first N natural
// numbers is divisible by 3
static boolean isDivisible(int N)
{
    // Check using the formula
    return (N - 1) % 3 != 0;
}

// Driver Code
public static void main(String[] args)
{
    // Given Number
    int N = 6;

    // Function Call
    if (isDivisible(N))
        System.out.println("Yes");

    else
        System.out.println("No");
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function that returns True if
# concatenation of first N natural
# numbers is divisible by 3
def isDivisible(N):

    # Check using the formula
    return (N - 1) % 3 != 0

# Driver Code
if __name__ == "__main__":

    # Given Number
    N = 6

    # Function Call
    if (isDivisible(N)):
        print("Yes")

    else:
        print("No")
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that returns True if
// concatenation of first N natural
// numbers is divisible by 3
static bool isDivisible(int N)
{
    // Check using the formula
    return (N – 1) % 3 != 0;
}

// Driver Code
public static void Main()
{
    // Given Number
    int N = 6;

    // Function Call
    if (isDivisible(N))
    Console.Write("Yes");

    else
    Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function that returns True if
// concatenation of first N natural
// numbers is divisible by 3
function isDivisible(N)
{
    // Check using the formula
    return (N - 1) % 3 != 0;
}

// Driver Code

// Given Number
var N = 6;

// Function Call
if (isDivisible(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Princi Singh.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*