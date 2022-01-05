# 两球可达性游戏

> 原文:[https://www.geeksforgeeks.org/two-balls-reachability-game/](https://www.geeksforgeeks.org/two-balls-reachability-game/)

给定白色的**号和黑色的**号。你需要有 **X** 数量的白球和 **Y** 数量的黑球(A < = X，B < = Y)通过做一些(零个或更多)的操作来赢得比赛。
*一次操作*:任何时候如果你有 p 白和 q 黑球，那么在那个时候你可以买 q 白或者 p 黑球。
看最后有没有可能有 X 白 Y 黑球。
**示例:****** 

```
Input:  A = 1, B = 1, X = 3, Y = 8
Output: POSSIBLE

Explanation:
The steps are, (1, 1)->(1, 2)->(3, 2)->(3, 5)->(3, 8)

Input: A = 3, Y = 2, X = 4, Y = 6
Output: NOT POSSIBLE
```

**方法:**
我们必须利用 gcd 的性质来解决这个问题。让我们看看如何。

1.  最初，我们有一个白色球和一个黑色球。我们必须得到剩下的 X-A 红球和 Y-B 黑球。

2.  下面是我们将使用的两个数字的 gcd 的属性，

```
gcd(x, y) = gcd(x + y, y)
gcd(x, y) = gcd(x, y + x)
```

2.  该属性与问题中提到的操作相同。因此，从这里，我们得到，如果最终状态的 gcd 与初始状态的 gcd 相同，那么它总是有可能达到目标，否则没有。

以下是上述方法的实现:

## C++

```
// C++ program to Find is it possible
// to have X white and Y black
// balls at the end.
#include <bits/stdc++.h>
using namespace std;

// Recursive function to return
// gcd of a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function returns if it's 
// possible to have X white
// and Y black balls or not.
void IsPossible(int a, int b,
                int x, int y)
{

    // Finding gcd of (x, y)
    // and (a, b)
    int final = gcd(x, y);
    int initial = gcd(a, b);

     // If gcd is same, it's always
    // possible to reach (x, y)
    if (initial == final)
    {

        cout << "POSSIBLE\n";
    }
    else
    {
        // Here it's never possible
        // if gcd is not same
        cout << "NOT POSSIBLE\n";
    }
}

// Driver Code
int main()
{

    int A = 1, B = 2, X = 4, Y = 11;
    IsPossible(A, B, X, Y);

    A = 2, B = 2, X = 3, Y = 6;
    IsPossible(A, B, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find is it possible
// to have X white and Y black
// balls at the end.
import java.io.*;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function returns if it's
// possible to have X white
// and Y black balls or not.
static void IsPossible(int a, int b,
                       int x, int y)
{

    // Finding gcd of (x, y)
    // and (a, b)
    int g = gcd(x, y);
    int initial = gcd(a, b);

    // If gcd is same, it's always
    // possible to reach (x, y)
    if (initial == g)
    {
        System.out.print("POSSIBLE\n");
    }
    else
    {
        // Here it's never possible
        // if gcd is not same
        System.out.print("NOT POSSIBLE\n");
    }
}

// Driver code
public static void main(String args[])
{
    int A = 1, B = 2, X = 4, Y = 11;
    IsPossible(A, B, X, Y);

    A = 2; B = 2; X = 3; Y = 6;
    IsPossible(A, B, X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to find is it possible
# to have X white and Y black
# balls at the end.

# Recursive function to return
# gcd of a and b
def gcd(a, b) :

    if (b == 0) :
        return a;
    return gcd(b, a % b);

# Function returns if it's
# possible to have X white
# and Y black balls or not.
def IsPossible(a, b, x, y) :

    # Finding gcd of (x, y)
    # and (a, b)
    final = gcd(x, y);
    initial = gcd(a, b);

    # If gcd is same, it's always
    # possible to reach (x, y)
    if (initial == final) :
        print("POSSIBLE");

    else :

        # Here it's never possible
        # if gcd is not same
        print("NOT POSSIBLE");

# Driver Code
if __name__ == "__main__" :

    A = 1; B = 2; X = 4; Y = 11;
    IsPossible(A, B, X, Y);

    A = 2; B = 2; X = 3; Y = 6;
    IsPossible(A, B, X, Y);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to Find is it possible
// to have X white and Y black
// balls at the end.
using System;
using System.Linq;

class GFG {

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function returns if it's
// possible to have X white
// and Y black balls or not.
static void IsPossible(int a, int b,
                       int x, int y)
{

    // Finding gcd of (x, y)
    // and (a, b)
    int g = gcd(x, y);
    int initial = gcd(a, b);

    // If gcd is same, it's always
    // possible to reach (x, y)
    if (initial == g)
    {
        Console.Write("POSSIBLE\n");
    }
    else
    {

        // Here it's never possible
        // if gcd is not same
        Console.Write("NOT POSSIBLE\n");
    }
}

// Driver code
static public void Main()
{
    int A = 1, B = 2;
    int X = 4, Y = 11;
    IsPossible(A, B, X, Y);

    A = 2; B = 2;
    X = 3; Y = 6;
    IsPossible(A, B, X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript program to Find is it possible
    // to have X white and Y black
    // balls at the end.

    // Recursive function to return 
    // gcd of a and b
    function gcd(a, b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function returns if it's  
    // possible to have X white 
    // and Y black balls or not.
    function IsPossible(a, b, x, y)
    {

        // Finding gcd of (x, y) 
        // and (a, b)
        let final = gcd(x, y);
        let initial = gcd(a, b);

         // If gcd is same, it's always
        // possible to reach (x, y)
        if (initial == final) 
        {

            document.write("POSSIBLE" + "</br>");
        }
        else
        {
            // Here it's never possible
            // if gcd is not same
            document.write("NOT POSSIBLE" + "</br>");
        }
    }

    let A = 1, B = 2, X = 4, Y = 11;
    IsPossible(A, B, X, Y);

    A = 2, B = 2, X = 3, Y = 6;
    IsPossible(A, B, X, Y);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
POSSIBLE
NOT POSSIBLE
```

时间复杂度:O(对数(最大值(A，B，X，Y))

辅助空间:0(1)