# 通过乘以 A 或除以 B 将 N 减 1 的最小运算

> 原文:[https://www . geesforgeks . org/min-operations-to-reduce-n-1 乘以 a 或除以 b/](https://www.geeksforgeeks.org/min-operations-to-reduce-n-to-1-by-multiplying-by-a-or-dividing-by-b/)

给定一个数字 **N** 和两个整数 **A** 和 **B** ，任务是检查是否可以通过以下两个操作将数字转换为 **1** :

*   乘以 A
*   除以 B

如果有可能将 **N** 减少到 **1** ，则打印实现它所需的最小操作次数，否则打印**-1”**。

**示例:**

> **输入:** N = 48，A = 3，B = 12
> **输出:** 3
> **说明:**
> 下面是 3 个操作:
> 1。48 除以 12 得 4。
> 2。4 乘以 3 得到 12。
> 3。12 除以 12 得 1。
> 因此操作总数为 3。
> 
> **输入:** N = 26，A = 3，B = 9
> **输出:** -1
> **说明:**
> 无法将 26 转换为 1。

**进场:**使用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。这个想法是检查 B 是否能被 A 整除，在此基础上，我们有以下观察结果:

*   如果 **B%A** **！= 0** ，那么只有当 **N** 完全被 **B** 整除，并且需要 **N/B 步骤**才能将 **N** 转换为 **1** 。而如果 **N = 1** 则需要 0 步，否则不可能打印**-1”**。
*   如果 **B%A == 0** ，那么考虑一个变量 **C** ，其值为 **B/A** ***。*** 用 B 除 **N，用第二次运算直到不能再除为止，我们把除法的个数叫做 **x.****
*   再把剩下的 **N** 除以 **C** 直到不能再除为止，我们把这个运算中的除法数叫做 **y.**
*   如果上述操作后 N 不等于 1，则无法使用上述操作将 **N** 转换为 **1** ，答案将是**-1”**，但如果它等于 1，则我们可以使用公式***total _ steps = x+(2 * y)***来计算所需的总最小步数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if it is possible
// to convert a number N to 1 by a minimum
// use of the two operations
int findIfPossible(int n, int a, int b)
{
    // For the Case b % a != 0
    if (b % a != 0) {

        // Check if n equal to 1
        if (n == 1)
            return 0;

        // Check if n is not
        // divisible by b
        else if (n % b != 0)
            return -1;
        else
            return (int)n / b;
    }

    // For the Case b % a == 0

    // Initialize a variable 'c'
    int c = b / a;
    int x = 0, y = 0;

    // Loop until n is divisible by b
    while (n % b == 0) {
        n = n / b;

        // Count number of divisions
        x++;
    }

    // Loop until n is divisible by c
    while (n % c == 0) {
        n = n / c;

        // Count number of operations
        y++;
    }

    // Check if n is reduced to 1
    if (n == 1) {

        // Count steps
        int total_steps = x + (2 * y);

        // Return the total number of steps
        return total_steps;
    }
    else
        return -1;
}

// Driver Code
int main()
{
    // Given n, a and b
    int n = 48;
    int a = 3, b = 12;

    // Function Call
    cout << findIfPossible(n, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if it is possible
// to convert a number N to 1 by a minimum
// use of the two operations
static int findIfPossible(int n, int a, int b)
{

    // For the Case b % a != 0
    if (b % a != 0)
    {

        // Check if n equal to 1
        if (n == 1)
            return 0;

        // Check if n is not
        // divisible by b
        else if (n % b != 0)
            return -1;
        else
            return (int)n / b;
    }

    // For the Case b % a == 0

    // Initialize a variable 'c'
    int c = b / a;
    int x = 0, y = 0;

    // Loop until n is divisible by b
    while (n % b == 0)
    {
        n = n / b;

        // Count number of divisions
        x++;
    }

    // Loop until n is divisible by c
    while (n % c == 0)
    {
        n = n / c;

        // Count number of operations
        y++;
    }

    // Check if n is reduced to 1
    if (n == 1)
    {

        // Count steps
        int total_steps = x + (2 * y);

        // Return the total number of steps
        return total_steps;
    }
    else
        return -1;
}

// Driver Code
public static void main(String s[])
{

    // Given n, a and b
    int n = 48;
    int a = 3, b = 12;

    // Function Call
    System.out.println(findIfPossible(n, a, b));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to convert a number N to 1 by a minimum
# use of the two operations
def FindIfPossible(n, a, b):

    # For the Case b % a != 0
    if (b % a) != 0:

    # Check if n equal to 1
        if n == 1:
            return 0

        # Check if n is not
        # divisible by b
        elif (n % b) != 0:
            return -1
        else:
            return int(n / b)

    # For the Case b % a == 0
    # Initialize a variable 'c'
    c = b / a
    x = 0
    y = 0

    # Loop until n is divisible by b
    while (n % b == 0):
        n /= b

    # Count number of divisions
        x += 1

    # Loop until n is divisible by c
    while (n % c == 0):
        n /= c

        # Count number of operations
        y += 1

    # Check if n is reduced to 1
    if n == 1:

        # Count steps
        total_steps = x + 2 * y

        # Return the total number of steps
        return total_steps
    else:
        return -1

# Driver code

# Given n, a and b
n = 48
a = 3
b = 12

print(FindIfPossible(n, a, b))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is possible
// to convert a number N to 1 by a minimum
// use of the two operations
static int findIfPossible(int n, int a, int b)
{

    // For the Case b % a != 0
    if (b % a != 0)
    {

        // Check if n equal to 1
        if (n == 1)
            return 0;

        // Check if n is not
        // divisible by b
        else if (n % b != 0)
            return -1;
        else
            return (int)n / b;
    }

    // For the Case b % a == 0

    // Initialize a variable 'c'
    int c = b / a;
    int x = 0, y = 0;

    // Loop until n is divisible by b
    while (n % b == 0)
    {
        n = n / b;

        // Count number of divisions
        x++;
    }

    // Loop until n is divisible by c
    while (n % c == 0)
    {
        n = n / c;

        // Count number of operations
        y++;
    }

    // Check if n is reduced to 1
    if (n == 1)
    {

        // Count steps
        int total_steps = x + (2 * y);

        // Return the total number of steps
        return total_steps;
    }
    else
        return -1;
}

// Driver Code
public static void Main()
{

    // Given n, a and b
    int n = 48;
    int a = 3, b = 12;

    // Function call
    Console.WriteLine(findIfPossible(n, a, b));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if it is possible
// to convert a number N to 1 by a minimum
// use of the two operations
function findIfPossible(n, a, b)
{

    // For the Case b % a != 0
    if (b % a != 0)
    {

        // Check if n equal to 1
        if (n == 1)
            return 0;

        // Check if n is not
        // divisible by b
        else if (n % b != 0)
            return -1;
        else
            return n / b;
    }

    // For the Case b % a == 0

    // Initialize a variable 'c'
    let c = b / a;
    let x = 0, y = 0;

    // Loop until n is divisible by b
    while (n % b == 0)
    {
        n = n / b;

        // Count number of divisions
        x++;
    }

    // Loop until n is divisible by c
    while (n % c == 0)
    {
        n = n / c;

        // Count number of operations
        y++;
    }

    // Check if n is reduced to 1
    if (n == 1)
    {

        // Count steps
        let total_steps = x + (2 * y);

        // Return the total number of steps
        return total_steps;
    }
    else
        return -1;
}

// Driver Code

       // Given n, a and b
    let n = 48;
    let a = 3, b = 12;

    // Function Call
    document.write(findIfPossible(n, a, b));

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(log(B/A))*
T5】辅助空间: *O(1)*