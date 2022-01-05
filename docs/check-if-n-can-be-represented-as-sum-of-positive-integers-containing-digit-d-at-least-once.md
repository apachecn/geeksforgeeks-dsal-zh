# 至少检查一次 N 是否可以表示为包含数字 D 的正整数之和

> 原文:[https://www . geesforgeks . org/check-if-n-可以表示为包含至少一次的数字 d 的正整数之和/](https://www.geeksforgeeks.org/check-if-n-can-be-represented-as-sum-of-positive-integers-containing-digit-d-at-least-once/)

给定一个正整数 **N** 和一个数字 **D** ，任务是检查 **N** 是否可以表示为包含数字 **D** 的正整数之和至少一次。如果可以用这样的格式表示 **N** ，那么打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 24，D = 7
> **输出:**是
> **说明:**值 24 可以表示为 17 + 7，均包含数字 7。
> 
> **输入:**N = 27D = 2
> T3】输出:是

**方法:**按照步骤解决问题:

*   [检查给定的 **N** 是否包含数字**D**T5。如果发现**为真**，则打印**“是”**。](https://www.geeksforgeeks.org/find-the-occurrences-of-y-in-the-range-of-x/)
*   否则，[迭代直到](https://www.geeksforgeeks.org/range-based-loop-c/) **N** 大于 **0** 并执行以下步骤:
    *   从 **N** 的值中减去 **D** 的值。
    *   [检查 **N** 的更新值是否包含数字**D**T5。如果发现**为真**，则打印**“是”**](https://www.geeksforgeeks.org/find-the-occurrences-of-y-in-the-range-of-x/)[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成以上步骤后，如果以上条件都不满足，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to check if N contains
// digit D in it
bool findDigit(int N, int D)
{
    // Iterate until N is positive
    while (N > 0) {

        // Find the last digit
        int a = N % 10;

        // If the last digit is the
        // same as digit D
        if (a == D) {
            return true;
        }

        N /= 10;
    }

    // Return false
    return false;
}

// Function to check if the value of
// N can be represented as sum of
// integers having digit d in it
bool check(int N, int D)
{
    // Iterate until N is positive
    while (N > 0) {

        // Check if N contains digit
        // D or not
        if (findDigit(N, D) == true) {
            return true;
        }

        // Subtracting D from N
        N -= D;
    }

    // Return false
    return false;
}

// Driver Code
int main()
{
    int N = 24;
    int D = 7;
    if (check(N, D)) {
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
// Java approach for the above approach
import java.util.*;

class GFG{

// Function to check if N contains
// digit D in it
static boolean findDigit(int N, int D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Find the last digit
        int a = N % 10;

        // If the last digit is the
        // same as digit D
        if (a == D)
        {
            return true;
        }
        N /= 10;
    }

    // Return false
    return false;
}

// Function to check if the value of
// N can be represented as sum of
// integers having digit d in it
static boolean check(int N, int D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Check if N contains digit
        // D or not
        if (findDigit(N, D) == true)
        {
            return true;
        }

        // Subtracting D from N
        N -= D;
    }

    // Return false
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int N = 24;
    int D = 7;

    if (check(N, D))
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

# Function to check if N contains
# digit D in it
def findDigit(N, D):

    # Iterate until N is positive
    while (N > 0):

        # Find the last digit
        a = N % 10

        # If the last digit is the
        # same as digit D
        if (a == D):
            return True

        N /= 10

    # Return false
    return False

# Function to check if the value of
# N can be represented as sum of
# integers having digit d in it
def check(N, D):

    # Iterate until N is positive
    while (N > 0):

        # Check if N contains digit
        # D or not
        if (findDigit(N, D) == True):
            return True

        # Subtracting D from N
        N -= D

    # Return false
    return False

# Driver Code
if __name__ == '__main__':

    N = 24
    D = 7

    if (check(N, D)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if N contains
// digit D in it
static bool findDigit(int N, int D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Find the last digit
        int a = N % 10;

        // If the last digit is the
        // same as digit D
        if (a == D)
        {
            return true;
        }
        N /= 10;
    }

    // Return false
    return false;
}

// Function to check if the value of
// N can be represented as sum of
// integers having digit d in it
static bool check(int N, int D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Check if N contains digit
        // D or not
        if (findDigit(N, D) == true)
        {
            return true;
        }

        // Subtracting D from N
        N -= D;
    }

    // Return false
    return false;
}

// Driver Code
public static void Main()
{
    int N = 24;
    int D = 7;

    if (check(N, D))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if N contains
// digit D in it
function findDigit(N, D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Find the last digit
        let a = N % 10;

        // If the last digit is the
        // same as digit D
        if (a == D)
        {
            return true;
        }
        N = Math.floor(N / 10);
    }

    // Return false
    return false;
}

// Function to check if the value of
// N can be represented as sum of
// integers having digit d in it
function check(N, D)
{

    // Iterate until N is positive
    while (N > 0)
    {

        // Check if N contains digit
        // D or not
        if (findDigit(N, D) == true)
        {
            return true;
        }

        // Subtracting D from N
        N -= D;
    }

    // Return false
    return false;
}

// Driver Code

    let N = 24;
    let D = 7;

    if (check(N, D))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*