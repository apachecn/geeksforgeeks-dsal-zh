# 通过重复将 X 乘以 2 或在末尾追加 1 将 X 转换为 Y

> 原文:[https://www . geeksforgeeks . org/convert-x-in-y-by-reply-x-with-2-or-appending-1-in-end/](https://www.geeksforgeeks.org/convert-x-into-y-by-repeatedly-multiplying-x-with-2-or-appending-1-at-the-end/)

给定两个正整数 **X** 和 **Y** ，任务是检查是否可以将数字 **X** 转换为 **Y** ，方法是将 **X** 乘以 **2** 或者在 **X** 的末尾追加 **1** 。如果可以将 **X** 转换为 **Y** ，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** X = 100，Y = 40021
> **输出:**是
> **说明:**
> 以下是将 X 转换为 Y 的操作:
> **操作 1:** 将 X(= 100)乘以 2，将 X 值修改为 200。
> **操作 2:** 在 X 末端追加 1(= 200)，将 X 值修改为 2001。
> **操作 3:** 将 X(= 2001)乘以 2，将 X 值修改为 4002。
> **操作 4:** 在 X 末端追加 1(= 4002)，将 X 值修改为 40021。
> 因此，从上面的操作可以看出，X 值可以转换为 y 值，因此，打印 Yes。
> 
> **输入:** X = 17，Y = 35
> **输出:**否

**方法:**给定的问题可以通过相反的方式执行操作来解决，即尝试将值 **Y** 转换为 **X** 。按照以下步骤解决问题:

*   [迭代直到 **Y** 的值大于 **X** 并执行以下步骤:](https://www.geeksforgeeks.org/range-based-loop-c/)
    *   如果 **Y** 的最后一位[的值为 1，那么将 **Y** 的值除以 **10** 。](https://www.geeksforgeeks.org/find-first-last-digits-number/)
    *   否则，如果 **Y** 的值可被 2 整除，则用 **2** 除 **Y** 。
    *   否则，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果 **Y** 的值与 **X** 的值相同，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if X can be
// converted to Y by multiplying
// X by 2 or appending 1 at the end
void convertXintoY(int X, int Y)
{
    // Iterate until Y is at least X
    while (Y > X) {

        // If Y is even
        if (Y % 2 == 0)
            Y /= 2;

        // If the last digit of Y is 1
        else if (Y % 10 == 1)
            Y /= 10;

        // Otherwise
        else
            break;
    }

    // Check if X is equal to Y
    if (X == Y)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int X = 100, Y = 40021;
    convertXintoY(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if X can be
// converted to Y by multiplying
// X by 2 or appending 1 at the end
static void convertXintoY(int X, int Y)
{
    // Iterate until Y is at least X
    while (Y > X) {

        // If Y is even
        if (Y % 2 == 0)
            Y /= 2;

        // If the last digit of Y is 1
        else if (Y % 10 == 1)
            Y /= 10;

        // Otherwise
        else
            break;
    }

    // Check if X is equal to Y
    if (X == Y)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int X = 100, Y = 40021;
    convertXintoY(X, Y);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if X can be
# converted to Y by multiplying
# X by 2 or appending 1 at the end
def convertXintoY(X, Y):
    # Iterate until Y is at least X
    while (Y > X):

        # If Y is even
        if (Y % 2 == 0):
            Y //= 2

        # If the last digit of Y is 1
        elif (Y % 10 == 1):
            Y //= 10

        # Otherwise
        else:
            break

    # Check if X is equal to Y
    if (X == Y):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    X,Y = 100, 40021
    convertXintoY(X, Y)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if X can be
// converted to Y by multiplying
// X by 2 or appending 1 at the end
static void convertXintoY(int X, int Y)
{

    // Iterate until Y is at least X
    while (Y > X) 
    {

        // If Y is even
        if (Y % 2 == 0)
            Y /= 2;

        // If the last digit of Y is 1
        else if (Y % 10 == 1)
            Y /= 10;

        // Otherwise
        else
            break;
    }

    // Check if X is equal to Y
    if (X == Y)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver Code
public static void Main(String[] args)
{
    int X = 100, Y = 40021;

    convertXintoY(X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

        // Function to check if X can be
        // converted to Y by multiplying
        // X by 2 or appending 1 at the end
        function convertXintoY(X, Y)
        {
            // Iterate until Y is at least X
            while (Y > X) {

                // If Y is even
                if (Y % 2 == 0)
                    Y = parseInt(Y / 2);

                // If the last digit of Y is 1
                else if (Y % 10 == 1)
                    Y = parseInt(Y /= 10);

                // Otherwise
                else
                    break;
            }

            // Check if X is equal to Y
            if (X == Y)
                document.write("Yes");
            else
                document.write("No");
        }

        // Driver Code
        let X = 100, Y = 40021;
        convertXintoY(X, Y);

  // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:** log(Y)*
***辅助空间:** O(1)*