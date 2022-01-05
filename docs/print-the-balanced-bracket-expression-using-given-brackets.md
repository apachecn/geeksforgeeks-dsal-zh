# 使用给定的括号

打印平衡括号表达式

> 原文:[https://www . geesforgeks . org/print-the-balanced-括号-expression-use-given-括号/](https://www.geeksforgeeks.org/print-the-balanced-bracket-expression-using-given-brackets/)

给定四个整数 **a** 、 **b** 、 **c** 和 **d** ，表示四种括号的数量。

1.  "(("
2.  "()"
3.  ")("
4.  "))"

任务是使用所有给定的括号打印任何平衡的括号表达式。如果我们不能形成一个平衡的括号表达式，那么打印 **-1** 。如果有多个答案，打印任意一个。
**例:**

> **输入:** a = 3，b = 1，c = 4，d = 3
> **输出:**((((((())())))))()
> **输入:** a = 3，b = 1，c = 4，d = 8
> **输出:** -1
> 给定的括号不可能有平衡的括号表达式。

**方法:**首先检查给定数量的括号是否能形成平衡括号表达式。如果类型 1 括号的数量等于类型 4 括号的数量，并且有任意数量的类型 3 括号，或者只有类型 2 括号，我们就可以形成表达式。因此组合条件为:

> (a = = d & & a)| |(a = = 0 & & c = = 0 & & d = = 0)

如果满足以上条件，可以按照以下步骤打印平衡括号表达式:

*   打印第 1 类括号的数量。
*   打印 3 型括号的数量。
*   打印第 4 类括号的数量。
*   打印第 2 类括号的数量。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print balanced bracket
// expression if it is possible
void printBalancedExpression(int a, int b, int c, int d)
{

    // If the condition is met
    if ((a == d && a) || (a == 0 && c == 0 && d == 0)) {

        // Print brackets of type-1
        for (int i = 1; i <= a; i++)
            cout << "((";

        // Print brackets of type-3
        for (int i = 1; i <= c; i++)
            cout << ")(";

        // Print brackets of type-4
        for (int i = 1; i <= d; i++)
            cout << "))";

        // Print brackets of type-2
        for (int i = 1; i <= b; i++)
            cout << "()";
    }

    // If the condition is not met
    else
        cout << -1;
}

// Driver code
int main()
{
    int a = 3, b = 1, c = 4, d = 3;
    printBalancedExpression(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to print balanced bracket
    // expression if it is possible
    static void printBalancedExpression(int a,
                            int b, int c, int d)
    {

        // If the condition is met
        if (((a == d) && (a != 0)) ||
        ((a == 0) && (c == 0) && (d == 0)))
        {

            // Print brackets of type-1
            for (int i = 1; i <= a; i++)
                System.out.print("((");

            // Print brackets of type-3
            for (int i = 1; i <= c; i++)
                System.out.print(")(");

            // Print brackets of type-4
            for (int i = 1; i <= d; i++)
                System.out.print("))");

            // Print brackets of type-2
            for (int i = 1; i <= b; i++)
                System.out.print("()");
        }

        // If the condition is not met
        else
            System.out.print(-1);
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 3, b = 1, c = 4, d = 3;
        printBalancedExpression(a, b, c, d);
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print balanced bracket
# expression if it is possible
def printBalancedExpression(a, b, c, d):

    # If the condition is met
    if ((a == d and a) or
        (a == 0 and c == 0 and d == 0)):

        # Print brackets of type-1
        for i in range(1, a + 1):
            print("((", end = "")

        # Print brackets of type-3
        for i in range(1, c + 1):
            print(")(", end = "")

        # Print brackets of type-4
        for i in range(1, d + 1):
            print("))", end = "")

        # Print brackets of type-2
        for i in range(1, b + 1):
            print("()", end = "")

    # If the condition is not met
    else:
        print("-1")

# Driver code
if __name__ == "__main__":

    a, b, c, d = 3, 1, 4, 3
    printBalancedExpression(a, b, c, d)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print balanced bracket
// expression if it is possible
static void printBalancedExpression(int a,
                        int b, int c, int d)
{

    // If the condition is met
    if (((a == d) && (a != 0)) ||
       ((a == 0) && (c == 0) && (d == 0)))
    {

        // Print brackets of type-1
        for (int i = 1; i <= a; i++)
            Console.Write("((");

        // Print brackets of type-3
        for (int i = 1; i <= c; i++)
            Console.Write(")(");

        // Print brackets of type-4
        for (int i = 1; i <= d; i++)
            Console.Write("))");

        // Print brackets of type-2
        for (int i = 1; i <= b; i++)
            Console.Write("()");
    }

    // If the condition is not met
    else
        Console.Write(-1);
}

// Driver code
public static void Main()
{
    int a = 3, b = 1, c = 4, d = 3;
    printBalancedExpression(a, b, c, d);
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

//PHP implementation of the approach
// Function to print balanced bracket
// expression if it is possible
function printBalancedExpression($a, $b, $c, $d)
{

    // If the condition is met
    if (($a == $d && $a) ||
       ($a == 0 && $c == 0 && $d == 0))
    {

        // Print brackets of type-1
        for ($i = 1; $i <= $a; $i++)
            echo "((";

        // Print brackets of type-3
        for ($i = 1; $i <= $c; $i++)
            echo ")(";

        // Print brackets of type-4
        for ($i = 1; $i <= $d; $i++)
            echo "))";

        // Print brackets of type-2
        for ($i = 1; $i <= $b; $i++)
            echo "()";
    }

    // If the condition is not met
    else
        echo -1;
}

    // Driver code
    $a = 3;
    $b = 1;
    $c = 4;
    $d = 3;
    printBalancedExpression($a, $b, $c, $d);

    // This code is contributed by jit_t

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to print balanced bracket
// expression if it is possible
    function printBalancedExpression(a , b , c , d)
    {

        // If the condition is met
        if (((a == d) && (a != 0)) || ((a == 0) &&
        (c == 0) && (d == 0))) {

            // Print brackets of type-1
            for (i = 1; i <= a; i++)
                document.write("((");

            // Print brackets of type-3
            for (i = 1; i <= c; i++)
                document.write(")(");

            // Print brackets of type-4
            for (i = 1; i <= d; i++)
                document.write("))");

            // Print brackets of type-2
            for (i = 1; i <= b; i++)
                document.write("()");
        }

        // If the condition is not met
        else
            document.write(-1);
    }

    // Driver code

        var a = 3, b = 1, c = 4, d = 3;
        printBalancedExpression(a, b, c, d);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
(((((()()()()())))))()
```