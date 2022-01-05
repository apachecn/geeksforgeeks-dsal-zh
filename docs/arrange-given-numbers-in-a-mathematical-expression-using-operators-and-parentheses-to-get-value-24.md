# 用运算符[+，-，*，/]和括号将给定的数字排列成数学表达式，得到数值 24

> 原文:[https://www . geeksforgeeks . org/array-给定数学表达式中的数字-使用运算符和括号来获取值-24/](https://www.geeksforgeeks.org/arrange-given-numbers-in-a-mathematical-expression-using-operators-and-parentheses-to-get-value-24/)

给定一个由**【1-9】**之间的 **4** 个整数组成的数组 **arr[]** ，任务是检查是否有可能通过将运算符 **+** 、**–**、 **/** 和 ***** 放置在数字之间或将它们用括号分组来获得数字 **24** 。如果可能，则打印“**可能**”，否则打印“**不可能”。**

**示例:**

> ***输入:** arr[] = {3，6，8，2}*
> ***输出:**可能*
> ***解释:***
> *得到 24 的一种可能方式是 3×6+8–2 = 24。*
> 
> ***输入:** arr[] = {7，2，10，6}*
> ***输出:**可能的*
> ***解释:***
> *得到 24 的一种可能方式是(7×2–10)x 6 = 24。*

**方法:**解决这个问题最简单的思路是基于[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)。按照以下步骤解决问题:

*   创建一个函数，比如**isnumberr24 possible(arr[])**，并在每个连续元素之间应用所有四个操作，然后[递归调用](https://www.geeksforgeeks.org/recursive-functions/)函数，比如**isnumberr24 possible util(op1，op2，op3)** ，该函数对 3 个数字执行所有可能的操作。
*   函数**是 Number24PossibleUtil(op1，op2，op3)** 在每个连续元素之间应用所有四个运算，并调用重载函数**是 Number24PossibleUtil(op1，op2)** ，它对两个数字应用运算。
*   功能**是 number 24 opsibleutil(op1，op2)** 用于检查给定的两个数字是否可以使用任何一个 **4** 操作，即 **+** 、**–**、 **/** 和 ***** 减少到 **24** 。尝试数字之间的每一个操作，如果其中任何一个操作导致 **24** 则返回**真**否则返回**假**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Division operation might loose some
// precision consider 0.001 as tolerance.
#define TOLERANCE 0.001

// This function is used to check whether
// given two number can reduce to 24 using
// any of the 4 operations
bool isNumber24PossibleUtil(double op1, double op2)
{
    // Check if any of the operation result to 24
    if (abs(op1 + op2 - 24.0) < TOLERANCE
        || abs(op1 - op2 - 24.0) < TOLERANCE
        || abs(op1 * op2 - 24.0) < TOLERANCE
        || op2 && abs(op1 / op2 - 24.0) < TOLERANCE)
        return true;
    return false;
}

// Function which applies all the possible operations
// in between all the parameters and call the function
// which check if given number can result in 24 or not
bool isNumber24PossibleUtil(double op1, double op2, double op3)
{
    // Applying operation between two operands reduces
    // the count of operands to two
    if (isNumber24PossibleUtil(op1 + op2, op3)
        || isNumber24PossibleUtil(op1 - op2, op3)
        || isNumber24PossibleUtil(op1 * op2, op3)
        || op2 && isNumber24PossibleUtil(op1 / op2, op3))
        return true;
    if (isNumber24PossibleUtil(op1, op2 + op3)
        || isNumber24PossibleUtil(op1, op2 - op3)
        || isNumber24PossibleUtil(op1, op2 * op3)
        || op3 && isNumber24PossibleUtil(op1, op2 / op3))
        return true;
    return false;
}

// Function takes given array as arr parameter
// and apply all possible operation in every
// consecutive elements and check if the remaining
// 3 parameters can be used for obtaining 24 or not
bool isNumber24Possible(int arr[])
{
    // Apply every operation between first two operands
    if (isNumber24PossibleUtil(arr[0] + arr[1], arr[2], arr[3])
        || isNumber24PossibleUtil(arr[0] - arr[1], arr[2], arr[3])
        || isNumber24PossibleUtil(arr[0] * arr[1], arr[2], arr[3])
        || arr[1] && isNumber24PossibleUtil(arr[0] / arr[1], arr[2], arr[3]))
        return true;
    // Between second and third operands
    if (isNumber24PossibleUtil(arr[0], arr[1] + arr[2], arr[3])
        || isNumber24PossibleUtil(arr[0], arr[1] - arr[2], arr[3])
        || isNumber24PossibleUtil(arr[0], arr[1] * arr[2], arr[3])
        || arr[2] && isNumber24PossibleUtil(arr[0], arr[1] / arr[2], arr[3]))
        return true;
    // Between third and fourth operands
    if (isNumber24PossibleUtil(arr[0], arr[1], arr[2] + arr[3])
        || isNumber24PossibleUtil(arr[0], arr[1], arr[2] - arr[3])
        || isNumber24PossibleUtil(arr[0], arr[1], arr[2] * arr[3])
        || arr[3] && isNumber24PossibleUtil(arr[0], arr[1], arr[2] / arr[3]))
        return true;

    return false;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 3, 6, 8, 2 };

    // Function Call
    if (isNumber24Possible(arr)) {
        cout << "Possible" << endl;
    }
    else {
        cout << "Not Possible" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Division operation might loose some
// precision consider 0.001 as tolerance.
static double TOLERANCE = 0.001;

// This function is used to check whether
// given two number can reduce to 24 using
// any of the 4 operations
static boolean isNumber24PossibleUtil(double op1,
                                      double op2)
{

    // Check if any of the operation result to 24
    if (Math.abs(op1 + op2 - 24.0) < TOLERANCE ||
        Math.abs(op1 - op2 - 24.0) < TOLERANCE ||
        Math.abs(op1 * op2 - 24.0) < TOLERANCE ||
        op2 != 0 && Math.abs(op1 / op2 - 24.0) < TOLERANCE)
        return true;
    return false;
}

// Function which applies all the possible operations
// in between all the parameters and call the function
// which check if given number can result in 24 or not
static boolean isNumber24PossibleUtil(double op1, double op2,
                                      double op3)
{

    // Applying operation between two operands reduces
    // the count of operands to two
    if (isNumber24PossibleUtil(op1 + op2, op3) ||
        isNumber24PossibleUtil(op1 - op2, op3) ||
        isNumber24PossibleUtil(op1 * op2, op3) ||
        op2 != 0 && isNumber24PossibleUtil(op1 / op2, op3))
        return true;
    if (isNumber24PossibleUtil(op1, op2 + op3) ||
        isNumber24PossibleUtil(op1, op2 - op3) ||
        isNumber24PossibleUtil(op1, op2 * op3) ||
        op3 != 0 && isNumber24PossibleUtil(op1, op2 / op3))
        return true;

    return false;
}

// Function takes given array as arr parameter
// and apply all possible operation in every
// consecutive elements and check if the remaining
// 3 parameters can be used for obtaining 24 or not
static boolean isNumber24Possible(int arr[])
{

    // Apply every operation between first two operands
    if (isNumber24PossibleUtil(arr[0] + arr[1], arr[2], arr[3]) ||
        isNumber24PossibleUtil(arr[0] - arr[1], arr[2], arr[3]) ||
        isNumber24PossibleUtil(arr[0] * arr[1], arr[2], arr[3]) ||
        arr[1] != 0 && isNumber24PossibleUtil(arr[0] / arr[1], arr[2],
                                              arr[3]))
        return true;
    // Between second and third operands
    if (isNumber24PossibleUtil(arr[0], arr[1] + arr[2], arr[3]) ||
        isNumber24PossibleUtil(arr[0], arr[1] - arr[2], arr[3]) ||
        isNumber24PossibleUtil(arr[0], arr[1] * arr[2], arr[3]) ||
        arr[2] != 0 && isNumber24PossibleUtil(arr[0], arr[1] / arr[2],
                                              arr[3]))
        return true;

    // Between third and fourth operands
    if (isNumber24PossibleUtil(arr[0], arr[1], arr[2] + arr[3]) ||
        isNumber24PossibleUtil(arr[0], arr[1], arr[2] - arr[3]) ||
        isNumber24PossibleUtil(arr[0], arr[1], arr[2] * arr[3]) ||
        arr[3] != 0 && isNumber24PossibleUtil(arr[0], arr[1],
                                              arr[2] / arr[3]))
        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 3, 6, 8, 2 };

    // Function Call
    if (isNumber24Possible(arr))
    {
        System.out.print("Possible");
    }
    else
    {
        System.out.print("Not Possible");
    }
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Division operation might loose some
# precision consider 0.001 as tolerance.
TOLERANCE = 0.001

# This function is used to check whether
# given two number can reduce to 24 using
# any of the 4 operations
def isNumber24PossibleUtill(op1, op2):

    # Check if any of the operation result to 24
    if (abs(op1 + op2 - 24.0) < TOLERANCE or
        abs(op1 - op2 - 24.0) < TOLERANCE or
        abs(op1 * op2 - 24.0) < TOLERANCE or
        op2 and abs(op1 / op2 - 24.0) < TOLERANCE):
        return True

    return False

# Function which applies all the possible operations
# in between all the parameters and call the function
# which check if given number can result in 24 or not
def isNumber24PossibleUtil(op1, op2, op3):

    # Applying operation between two operands reduces
    # the count of operands to two
    if ((isNumber24PossibleUtill(op1 + op2, op3)) or
        (isNumber24PossibleUtill(op1 - op2, op3)) or
        (isNumber24PossibleUtill(op1 * op2, op3)) or
        (op2 and isNumber24PossibleUtill(op1 / op2, op3))):
        return True

    if (isNumber24PossibleUtill(op1, op2 + op3) or
        isNumber24PossibleUtill(op1, op2 - op3) or
        isNumber24PossibleUtill(op1, op2 * op3) or
        op3 and isNumber24PossibleUtill(op1, op2 / op3)):
        return True

    return False

# Function takes given array as arr parameter
# and apply all possible operation in every
# consecutive elements and check if the remaining
# 3 parameters can be used for obtaining 24 or not
def isNumber24Possible(arr):

    # Apply every operation between first two operands
    if (isNumber24PossibleUtil(arr[0] + arr[1],
                               arr[2], arr[3]) or
        isNumber24PossibleUtil(arr[0] - arr[1],
                               arr[2], arr[3]) or
        isNumber24PossibleUtil(arr[0] * arr[1],
                               arr[2], arr[3]) or
                               arr[1] and
        isNumber24PossibleUtil(arr[0] / arr[1],
                               arr[2], arr[3])):
        return True

    # Between second and third operands
    if (isNumber24PossibleUtil(arr[0], arr[1] + arr[2], arr[3]) or
        isNumber24PossibleUtil(arr[0], arr[1] - arr[2], arr[3]) or
        isNumber24PossibleUtil(arr[0], arr[1] * arr[2], arr[3]) or
        arr[2] and isNumber24PossibleUtil(arr[0], arr[1] / arr[2],
                                          arr[3])):
        return True

    # Between third and fourth operands
    if (isNumber24PossibleUtil(arr[0], arr[1], arr[2] + arr[3]) or
        isNumber24PossibleUtil(arr[0], arr[1], arr[2] - arr[3]) or
        isNumber24PossibleUtil(arr[0], arr[1], arr[2] * arr[3]) or
        arr[3] and isNumber24PossibleUtil(arr[0], arr[1],
                                          arr[2] / arr[3])):
        return True

    return False

# Driver Code

# Given Input
arr = [ 3, 6, 8, 2 ]

# Function Call
if (isNumber24Possible(arr)):
    print("Possible")
else:
    print("Not Possible")

# This code is contributed by sanjoy_62
```

## C#

```
using System;

public class GFG {

    static double TOLERANCE = 0.001;

    // This function is used to check whether
    // given two number can reduce to 24 using
    // any of the 4 operations
    static bool isNumber24PossibleUtil(double op1,
                                          double op2)
    {

        // Check if any of the operation result to 24
        if (Math.Abs(op1 + op2 - 24.0) < TOLERANCE
            || Math.Abs(op1 - op2 - 24.0) < TOLERANCE
            || Math.Abs(op1 * op2 - 24.0) < TOLERANCE
            || op2 != 0
                   && Math.Abs(op1 / op2 - 24.0)
                          < TOLERANCE)
            return true;
        return false;
    }

    // Function which applies all the possible operations
    // in between all the parameters and call the function
    // which check if given number can result in 24 or not
    static bool isNumber24PossibleUtil(double op1,
                                          double op2,
                                          double op3)
    {

        // Applying operation between two operands reduces
        // the count of operands to two
        if (isNumber24PossibleUtil(op1 + op2, op3)
            || isNumber24PossibleUtil(op1 - op2, op3)
            || isNumber24PossibleUtil(op1 * op2, op3)
            || op2 != 0
                   && isNumber24PossibleUtil(op1 / op2,
                                             op3))
            return true;
        if (isNumber24PossibleUtil(op1, op2 + op3)
            || isNumber24PossibleUtil(op1, op2 - op3)
            || isNumber24PossibleUtil(op1, op2 * op3)
            || op3 != 0
                   && isNumber24PossibleUtil(op1,
                                             op2 / op3))
            return true;

        return false;
    }

    // Function takes given array as arr parameter
    // and apply all possible operation in every
    // consecutive elements and check if the remaining
    // 3 parameters can be used for obtaining 24 or not
    static bool isNumber24Possible(int[] arr)
    {

        // Apply every operation between first two operands
        if (isNumber24PossibleUtil(arr[0] + arr[1], arr[2],
                                   arr[3])
            || isNumber24PossibleUtil(arr[0] - arr[1],
                                      arr[2], arr[3])
            || isNumber24PossibleUtil(arr[0] * arr[1],
                                      arr[2], arr[3])
            || arr[1] != 0
                   && isNumber24PossibleUtil(
                       arr[0] / arr[1], arr[2], arr[3]))
            return true;
        // Between second and third operands
        if (isNumber24PossibleUtil(arr[0], arr[1] + arr[2],
                                   arr[3])
            || isNumber24PossibleUtil(
                arr[0], arr[1] - arr[2], arr[3])
            || isNumber24PossibleUtil(
                arr[0], arr[1] * arr[2], arr[3])
            || arr[2] != 0
                   && isNumber24PossibleUtil(
                       arr[0], arr[1] / arr[2], arr[3]))
            return true;

        // Between third and fourth operands
        if (isNumber24PossibleUtil(arr[0], arr[1],
                                   arr[2] + arr[3])
            || isNumber24PossibleUtil(arr[0], arr[1],
                                      arr[2] - arr[3])
            || isNumber24PossibleUtil(arr[0], arr[1],
                                      arr[2] * arr[3])
            || arr[3] != 0
                   && isNumber24PossibleUtil(
                       arr[0], arr[1], arr[2] / arr[3]))
            return true;

        return false;
    }
    static public void Main()
    {
        int[] arr = { 3, 6, 8, 2 };

        // Function Call
        if (isNumber24Possible(arr)) {
            Console.WriteLine("Possible");
        }
        else {
            Console.WriteLine("Not Possible");
        }
    }
}

// This code is contributed by maddler.
```

**Output**

```
Possible
```

***时间复杂度:** O(4 <sup>2</sup> × 4！)*
***辅助空间:** O(1)*