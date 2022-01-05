# 构造一个元素不超过 X，相邻两个元素之和不超过 Y 的矩阵

> 原文:[https://www . geeksforgeeks . org/construct-a-无元素超 x 和两个相邻元素之和-不超 y/](https://www.geeksforgeeks.org/construct-a-matrix-with-no-element-exceeding-x-and-sum-of-two-adjacent-elements-not-exceeding-y/)

给定四个整数 **N** 、 **M** 、 **X** 和 **Y** ，任务是构造一个 **N * M 矩阵**，使得每个单元格由范围**【0，X】**中的一个值组成，使得任意两个相邻单元格的和应该小于或等于 **Y** ，并且该矩阵的总和应该最大。

**示例:**

> **输入:** N = 3，M = 3，X = 5，Y = 3
> **输出:**
> 3 0 3
> 0 3 0
> 3 0 3
> **说明:**
> 矩阵的所有值都在 0 到 5 之间。
> 任意两个相邻单元格之和等于 3。
> 矩阵的总和为 15，这是最大可能。
> 
> **输入:** N = 3，M = 3，X = 3，Y = 5
> **输出:**
> 3 2 3
> 2 3 2
> 3 2 3

**方法:**
按照以下步骤解决问题:

*   为了满足两个必要条件，矩阵只需要交替填充以下两个数字:

> 第一个数=最小值(X，Y)
> 第二个数=最小值(2X，Y)–第一个数
> **插图:**
> N = 3，M = 3，X = 5，Y = 3
> 第一个数=最小值(X，Y) =最小值(5，3) = 3
> 第二个数=最小值(2X，Y)–3 =最小值(10，3)–3 = 3–3 = 0
> 因此，任意两个相邻单元格的和= 3 + 0 = 3(= Y)

*   最后，交替打印两个数字，第一个数字后跟第二个数字，以最大化矩阵的总和。

下面是上述方法的实现。

## C++

```
// C++ implementation of
// the above approach
#include <iostream>
using namespace std;

// Function to print the
// required matrix
void FindMatrix(int n, int m,
                int x, int y)
{
    int a, b, i, j;

    // For 1*1 matrix
    if (n * m == 1) {
        if (x > y) {
            cout << y << "\n";
        }
        else {
            cout << x << "\n";
        }
        return;
    }

    // Greater number
    a = min(x, y);

    // Smaller number
    b = min(2 * x, y) - a;

    // Sets/Resets for alternate
    // filling of the matrix
    bool flag = true;

    // Print the matrix
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            if (flag)
                cout << a << ' ';
            else
                cout << b << ' ';
            flag = !flag;
        }

        // If end of row is reached
        if (((n % 2 != 0 && m % 2 == 0)
             || (n % 2 == 0 && m % 2 == 0)))
            flag = !flag;
        cout << "\n";
    }
}

// Driver Code
int main()
{

    int N, M, X, Y;
    N = 3;
    M = 3;
    X = 5;
    Y = 3;
    FindMatrix(N, M, X, Y);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

// Function to print the
// required matrix
static void FindMatrix(int n, int m,
                       int x, int y)
{
    int a, b, i, j;

    // For 1*1 matrix
    if (n * m == 1)
    {
        if (x > y)
        {
            System.out.print(y + "\n");
        }
        else
        {
            System.out.print(x + "\n");
        }
        return;
    }

    // Greater number
    a = Math.min(x, y);

    // Smaller number
    b = Math.min(2 * x, y) - a;

    // Sets/Resets for alternate
    // filling of the matrix
    boolean flag = true;

    // Print the matrix
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
        {
            if (flag)
                System.out.print(a + " ");
            else
                System.out.print(b + " ");
            flag = !flag;
        }

        // If end of row is reached
        if (((n % 2 != 0 && m % 2 == 0) ||
             (n % 2 == 0 && m % 2 == 0)))
            flag = !flag;
        System.out.print("\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N, M, X, Y;
    N = 3;
    M = 3;
    X = 5;
    Y = 3;
    FindMatrix(N, M, X, Y);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to print the
# required matrix
def FindMatrix(n, m, x, y):

    # For 1*1 matrix
    if (n * m == 1):
        if (x > y):
            print(y)
        else:
            print(x)

        return

    # Greater number
    a = min(x, y)

    # Smaller number
    b = min(2 * x, y) - a

    # Sets/Resets for alternate
    # filling of the matrix
    flag = True

    # Print the matrix
    for i in range(n):
        for j in range(m):

            if (flag):
                print(a, end = " ")
            else:
                print(b, end = " ")

            flag = not flag

        # If end of row is reached
        if (((n % 2 != 0 and m % 2 == 0) or
             (n % 2 == 0 and m % 2 == 0))):
            flag = not flag

        print ()

# Driver Code
N = 3
M = 3
X = 5
Y = 3

FindMatrix(N, M, X, Y)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to print the
// required matrix
static void FindMatrix(int n, int m,
                       int x, int y)
{
    int a, b, i, j;

    // For 1*1 matrix
    if (n * m == 1)
    {
        if (x > y)
        {
            Console.Write(y + "\n");
        }
        else
        {
            Console.Write(x + "\n");
        }
        return;
    }

    // Greater number
    a = Math.Min(x, y);

    // Smaller number
    b = Math.Min(2 * x, y) - a;

    // Sets/Resets for alternate
    // filling of the matrix
    bool flag = true;

    // Print the matrix
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
        {
            if (flag)
                Console.Write(a + " ");
            else
                Console.Write(b + " ");
            flag = !flag;
        }

        // If end of row is reached
        if (((n % 2 != 0 && m % 2 == 0) ||
             (n % 2 == 0 && m % 2 == 0)))
            flag = !flag;
        Console.Write("\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N, M, X, Y;
    N = 3;
    M = 3;
    X = 5;
    Y = 3;
    FindMatrix(N, M, X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to print the
// required matrix
function FindMatrix(n, m, x, y)
{
    var a, b, i, j;

    // For 1*1 matrix
    if (n * m == 1)
    {
        if (x > y)
        {
            document.write(y);
        }
        else
        {
            document.write(x);
        }
        return;
    }

    // Greater number
    a = Math.min(x, y);

    // Smaller number
    b = Math.min(2 * x, y) - a;

    // Sets/Resets for alternate
    // filling of the matrix
    var flag = true;

    // Print the matrix
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
        {
            if (flag)
                document.write(a + " ");
            else
                document.write(b + " ");

            flag = !flag;
        }

        // If end of row is reached
        if (((n % 2 != 0 && m % 2 == 0) ||
             (n % 2 == 0 && m % 2 == 0)))
            flag = !flag;

        document.write("<br>");
    }
}

// Driver Code
var N, M, X, Y;
N = 3;
M = 3;
X = 5;
Y = 3;

FindMatrix(N, M, X, Y);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
3 0 3 
0 3 0 
3 0 3
```

***时间复杂度:** O(N * M)*
***空间复杂度:** O(1)*