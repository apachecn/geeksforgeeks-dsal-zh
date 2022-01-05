# 检查两点(x1，y1)和(x2，y2)是否位于给定直线的同一侧

> 原文:[https://www . geesforgeks . org/check-two-point-x1-y1-和-x2-y2-同侧躺在给定线路上-或-否/](https://www.geeksforgeeks.org/check-whether-two-points-x1-y1-and-x2-y2-lie-on-same-side-of-a-given-line-or-not/)

给定三个整数 **a** 、 **b** 和 **c** ，表示一条直线的方程的系数**a * x+b * y–c = 0**。给定两个整数点 **(x1，y1)** 和 **(x2，y2)** 。任务是确定点 **(x1，y1)** 和 **(x2，y2)** 是否位于给定直线的同一侧。
**举例:**

> **输入:** a = 1，b = 1，c = 1，x1 = 1，y1 = 1，x2 = 1，y2 = 2
> **输出:**是
> 在 a * x+b * y–c 上应用(x1，y1)和(x2，y2)时，分别给出 1 和 2，这两个点具有相同的符号，因此这两个点位于直线的同一侧。
> **输入:** a = 1，b = 1，c = 1，x1 = 1，y1 = 1，x2 = 0，y2 = 0
> **输出:**否

**方法:**应用给定线方程上的两个点，检查获得的值是否属于相同的奇偶性。
以下是上述办法的实施情况:

## C++

```
// C++ program to check if two points
// lie on the same side or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if two points
// lie on the same side or not
bool pointsAreOnSameSideOfLine(int a, int b, int c,
                        int x1,    int y1, int x2, int y2)
{
    int fx1; // Variable to store a * x1 + b * y1 - c
    int fx2; // Variable to store a * x2 + b * y2 - c

    fx1 = a * x1 + b * y1 - c;
    fx2 = a * x2 + b * y2 - c;

    // If fx1 and fx2 have same sign
    if ((fx1 * fx2) > 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int a = 1, b = 1, c = 1;
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 1;

    if (pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two points
// lie on the same side or not
import java.util.*;

class GFG
{

// Function to check if two points
// lie on the same side or not
static boolean pointsAreOnSameSideOfLine(int a, int b,
                                         int c, int x1,
                                         int y1, int x2,
                                         int y2)
{
    int fx1; // Variable to store a * x1 + b * y1 - c
    int fx2; // Variable to store a * x2 + b * y2 - c

    fx1 = a * x1 + b * y1 - c;
    fx2 = a * x2 + b * y2 - c;

    // If fx1 and fx2 have same sign
    if ((fx1 * fx2) > 0)
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int a = 1, b = 1, c = 1;
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 1;

    if (pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if two points
# lie on the same side or not

# Function to check if two points
# lie on the same side or not
def pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2):
    fx1 = 0 # Variable to store a * x1 + b * y1 - c
    fx2 = 0 # Variable to store a * x2 + b * y2 - c

    fx1 = a * x1 + b * y1 - c
    fx2 = a * x2 + b * y2 - c

    # If fx1 and fx2 have same sign
    if ((fx1 * fx2) > 0):
        return True

    return False

# Driver code
a, b, c = 1, 1, 1
x1, y1 = 1, 1
x2, y2 = 2, 1

if (pointsAreOnSameSideOfLine(a, b, c,
                              x1, y1, x2, y2)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if two points
// lie on the same side or not
using System;
class GFG
{

// Function to check if two points
// lie on the same side or not
static bool pointsAreOnSameSideOfLine(int a, int b,
                                      int c, int x1,
                                      int y1, int x2,
                                      int y2)
{
    int fx1; // Variable to store a * x1 + b * y1 - c
    int fx2; // Variable to store a * x2 + b * y2 - c

    fx1 = a * x1 + b * y1 - c;
    fx2 = a * x2 + b * y2 - c;

    // If fx1 and fx2 have same sign
    if ((fx1 * fx2) > 0)
        return true;

    return false;
}

// Driver code
public static void Main()
{
    int a = 1, b = 1, c = 1;
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 1;

    if (pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
    // Javascript program to check if two points 
    // lie on the same side or not

    // Function to check if two points 
    // lie on the same side or not
    function pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2)
    {
        let fx1; // Variable to store a * x1 + b * y1 - c
        let fx2; // Variable to store a * x2 + b * y2 - c

        fx1 = a * x1 + b * y1 - c;
        fx2 = a * x2 + b * y2 - c;

        // If fx1 and fx2 have same sign
        if ((fx1 * fx2) > 0)
            return true;

        return false;
    }

    let a = 1, b = 1, c = 1;
    let x1 = 1, y1 = 1;
    let x2 = 2, y2 = 1;

    if (pointsAreOnSameSideOfLine(a, b, c, x1, y1, x2, y2))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
Yes
```