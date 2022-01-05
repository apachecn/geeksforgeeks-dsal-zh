# 求给定方程中 X 和 Y 的值

> 原文:[https://www . geesforgeks . org/find-给定方程中 x 和 y 的值/](https://www.geeksforgeeks.org/find-the-values-of-x-and-y-in-the-given-equations/)

给定两个数字![A  ](img/d87f1cb8a8e09ef6d976b963803548e2.png "Rendered by QuickLaTeX.com")和![B  ](img/af5280b6d00ec107c9fc36bb5fe47e67.png "Rendered by QuickLaTeX.com")。求方程中 **X** 和 **Y** 的值。

1.  A = X + Y
2.  B = X 异或 Y

**任务**是让 X 尽可能最小。如果无法找到 X 和 Y 的任何有效值，则打印-1。
**例:**

```
Input : A = 12, B = 8
Output : X = 2, Y = 10

Input : A = 12, B = 9
Output : -1
```

让我们看看 X 中的某个位，它等于 1。如果 Y 中的相应位等于 0，则可以交换这两个位，从而减少 X 和增加 Y，而不改变它们的总和和异或。我们可以得出结论，如果 X 中的某个位等于 1，那么 Y 中的相应位也等于 1。这样，Y = X + B .考虑到 X + Y = X + X + B = A，我们可以得到以下求 X 和 Y 的公式:

*   x =(A–B)/2
*   Y = X + B = (A + B) / 2

人们还应该注意到，如果 **A < B** 或者 A 和 B 具有不同的奇偶性，那么答案不存在，输出为-1。如果 X 和(A–X)不等于 X，那么答案也是-1。
以下是上述办法的实施情况:

## C++

```
// CPP program to find the values of
// X and Y using the given equations

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// values of X and Y
void findValues(int a, int b)
{
    // base condition
    if ((a - b) % 2 == 1) {
        cout << "-1";
        return;
    }

    // required answer
    cout << (a - b) / 2 << " " << (a + b) / 2;
}

// Driver Code
int main()
{
    int a = 12, b = 8;

    findValues(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the values of
// X and Y using the given equations
import java.io.*;

class GFG
{

// Function to find the
// values of X and Y
static void findValues(int a, int b)
{
    // base condition
    if ((a - b) % 2 == 1)
    {
            System.out.println ("-1");
        return;
    }

    // required answer
    System.out.println (((a - b) / 2)+ " " +
                            ((a + b) / 2));
}

    // Driver Code
    public static void main (String[] args)
    {
        int a = 12, b = 8;
        findValues(a, b);
    }
}

// This code is contributed by ajit...
```

## 蟒蛇 3

```
# Python3 program to find the values of
# X and Y using the given equations

# Function to find the values of X and Y
def findValues(a, b):

    # base condition
    if ((a - b) % 2 == 1):
        print("-1");
        return;

    # required answer
    print((a - b) // 2, (a + b) // 2);

# Driver Code
a = 12; b = 8;

findValues(a, b);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to find the values of
// X and Y using the given equations
using System;

class GFG
{

// Function to find the
// values of X and Y
static void findValues(int a, int b)
{
    // base condition
    if ((a - b) % 2 == 1)
    {
            Console.Write ("-1");
        return;
    }

    // required answer
    Console.WriteLine(((a - b) / 2)+ " " +
                        ((a + b) / 2));
}

// Driver Code
static public void Main ()
{
    int a = 12, b = 8;
    findValues(a, b);
}
}

// This code is contributed by @Tushil..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the values of
// X and Y using the given equations

// Function to find the values
// of X and Y
function findValues($a, $b)
{
    // base condition
    if (($a - $b) % 2 == 1)
    {
        echo "-1";
        return;
    }

    // required answer
    echo ($a - $b) / 2, " " ,
         ($a + $b) / 2;
}

// Driver Code
$a = 12;
$b = 8;
findValues($a, $b);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to find the values of
// X and Y using the given equations

// Function to find the values
// of X and Y
function findValues(a, b)
{
    // base condition
    if ((a - b) % 2 == 1)
    {
        document.write( "-1");
        return;
    }

    // required answer
    document.write( (a - b) / 2+ " " +
        (a + b) / 2);
}

// Driver Code
let a = 12;
let b = 8;
findValues(a, b);

// This code is contributed
// by bobby

</script>
```

**Output:** 

```
2 10
```