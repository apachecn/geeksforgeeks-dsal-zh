# 求两个数的和并异或|集合 2

> 原文:[https://www . geeksforgeeks . org/find-two-numbers-from-sum-and-xor-set-2/](https://www.geeksforgeeks.org/find-two-numbers-from-their-sum-and-xor-set-2/)

给定两个整数 **X** 和 **Y** ，任务是找出两个整数之和 **X** 和[按位异或](https://www.geeksforgeeks.org/tag/xor/)等于 **Y** 。

**示例:**

> **输入:** X = 17，Y = 13
> **输出:** 2 15
> **解释:** 2 + 15 = 17 和 2 ^ 15 = 13
> 
> **输入:** X = 1870807699，Y = 259801747
> T3】输出: 805502976 1065304723

**天真的做法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/find-two-numbers-sum-xor/)了解解决问题最简单的方法。

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> *a+b =(a ^ b)+2 *(a&b)*
> *=>x = y+2 *(a&b)*
> 
> *计算和时，如果两个位都是 **1** (即 and 为 1)，则合成位为 **0** ， **1** 相加为进位，这意味着**和**中的每一位都是* [*左移*](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)*1，即 AND 的值乘以 2 相加。*
> 
> *重新排列各项，得到表达式(A&B)=(X–Y)/2。*
> 
> 这验证了上述观察。

存在以下情况:

*   **如果 X < Y:** 在这种情况下，解不存在，因为(A & B)变为负，这是不可能的。
*   **如果 X–Y 是奇数:**在这种情况下，解不存在，因为(X–Y)不能被 2 整除。
*   **如果 X = Y:** 在这种情况下，A & B = 0。因此，A 的最小值应为 0，B 的值应为 Y，以满足给定的方程。
*   **否则:**A&B =(X–Y)/2 满足，前提是((X–Y)/2)&Y 等于 0。如果为真，则 A =(X–Y)/2 和 B = A + Y。否则，A = -1 和 B = -1。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of A and
// B whose sum is X and xor is Y
void findNums(int X, int Y)
{

    // Initialize the two numbers
    int A, B;

    // Case 1: X < Y
    if (X < Y) {
        A = -1;
        B = -1;
    }

    // Case 2: X-Y is odd
    else if (abs(X - Y) & 1) {
        A = -1;
        B = -1;
    }

    // Case 3: If both Sum and XOR
    // are equal
    else if (X == Y) {
        A = 0;
        B = Y;
    }

    // Case 4: If above cases fails
    else {

        // Update the value of A
        A = (X - Y) / 2;

        // Check if A & Y value is 0
        if ((A & Y) == 0) {

            // If true, update B
            B = (A + Y);
        }

        // Otherwise assign -1 to A,
        // -1 to B
        else {
            A = -1;
            B = -1;
        }
    }

    // Print the numbers A and B
    cout << A << " " << B;
}

// Driver Code
int main()
{
    // Given Sum and XOR of 2 numbers
    int X = 17, Y = 13;

    // Function Call
    findNums(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the value of A and
// B whose sum is X and xor is Y
static void findNums(int X, int Y)
{

    // Initialize the two numbers
    int A, B;

    // Case 1: X < Y
    if (X < Y)
    {
        A = -1;
        B = -1;
    }

    // Case 2: X-Y is odd
    else if (((Math.abs(X - Y)) & 1) != 0)
    {
        A = -1;
        B = -1;
    }

    // Case 3: If both Sum and XOR
    // are equal
    else if (X == Y)
    {
        A = 0;
        B = Y;
    }

    // Case 4: If above cases fails
    else
    {

        // Update the value of A
        A = (X - Y) / 2;

        // Check if A & Y value is 0
        if ((A & Y) == 0)
        {

            // If true, update B
            B = (A + Y);
        }

        // Otherwise assign -1 to A,
        // -1 to B
        else
        {
            A = -1;
            B = -1;
        }
    }

    // Print the numbers A and B
    System.out.print(A + " " + B);
}

// Driver Code
public static void main(String[] args)
{

    // Given Sum and XOR of 2 numbers
    int X = 17, Y = 13;

    // Function Call
    findNums(X, Y);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 计算机编程语言

```
# Python program for the above approach

# Function to find the value of A and
# B whose sum is X and xor is Y
def findNums(X, Y):

    # Initialize the two numbers
    A = 0;
    B = 0;

    # Case 1: X < Y
    if (X < Y):
        A = -1;
        B = -1;

    # Case 2: X-Y is odd
    elif (((abs(X - Y)) & 1) != 0):
        A = -1;
        B = -1;

    # Case 3: If both Sum and XOR
    # are equal
    elif (X == Y):
        A = 0;
        B = Y;

    # Case 4: If above cases fails
    else:

        # Update the value of A
        A = (X - Y) // 2;

        # Check if A & Y value is 0
        if ((A & Y) == 0):

            # If True, update B
            B = (A + Y);

        # Otherwise assign -1 to A,
        # -1 to B
        else:
            A = -1;
            B = -1;

    # Print the numbers A and B
    print A;
    print B;

# Driver Code
if __name__ == '__main__':

    # Given Sum and XOR of 2 numbers
    X = 17;
    Y = 13;

    # Function Call
    findNums(X, Y);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the value of A and
// B whose sum is X and xor is Y
static void findNums(int X, int Y)
{

    // Initialize the two numbers
    int A, B;

    // Case 1: X < Y
    if (X < Y)
    {
        A = -1;
        B = -1;
    }

    // Case 2: X-Y is odd
    else if (((Math.Abs(X - Y)) & 1) != 0)
    {
        A = -1;
        B = -1;
    }

    // Case 3: If both Sum and XOR
    // are equal
    else if (X == Y)
    {
        A = 0;
        B = Y;
    }

    // Case 4: If above cases fails
    else
    {

        // Update the value of A
        A = (X - Y) / 2;

        // Check if A & Y value is 0
        if ((A & Y) == 0)
        {

            // If true, update B
            B = (A + Y);
        }

        // Otherwise assign -1 to A,
        // -1 to B
        else
        {
            A = -1;
            B = -1;
        }
    }

    // Print the numbers A and B
    Console.Write(A + " " + B);
}

// Driver Code
public static void Main(String[] args)
{

    // Given Sum and XOR of 2 numbers
    int X = 17, Y = 13;

    // Function Call
    findNums(X, Y);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to find the value of A and
// B whose sum is X and xor is Y
function findNums(X, Y)
{

    // Initialize the two numbers
    let A, B;

    // Case 1: X < Y
    if (X < Y) {
        A = -1;
        B = -1;
    }

    // Case 2: X-Y is odd
    else if (Math.abs(X - Y) & 1) {
        A = -1;
        B = -1;
    }

    // Case 3: If both Sum and XOR
    // are equal
    else if (X == Y) {
        A = 0;
        B = Y;
    }

    // Case 4: If above cases fails
    else {

        // Update the value of A
        A = (X - Y) / 2;

        // Check if A & Y value is 0
        if ((A & Y) == 0) {

            // If true, update B
            B = (A + Y);
        }

        // Otherwise assign -1 to A,
        // -1 to B
        else {
            A = -1;
            B = -1;
        }
    }

    // Print the numbers A and B
    document.write(A + " " + B);
}

// Driver Code

    // Given Sum and XOR of 2 numbers
    let X = 17, Y = 13;

    // Function Call
    findNums(X, Y);

</script>
```

**Output:** 

```
2 15
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)