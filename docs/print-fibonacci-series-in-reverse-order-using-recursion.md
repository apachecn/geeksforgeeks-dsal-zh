# 使用递归以逆序打印斐波那契数列

> 原文:[https://www . geesforgeks . org/print-Fibonacci-逆序数列-使用递归/](https://www.geeksforgeeks.org/print-fibonacci-series-in-reverse-order-using-recursion/)

给定一个整数 **N，**任务是使用[递归](https://www.geeksforgeeks.org/recursion/)以相反的顺序打印斐波那契数列的[第一个 **N** 项。](https://www.geeksforgeeks.org/print-fibonacci-series-reverse-order/)

**示例:**

> **输入:** N = 5
> **输出:**3 2 1 1 0
> T6】说明:前五项为–0 1 2 3。
> 
> **输入:**N = 10
> T3】输出: 34 21 13 8 5 3 2 1 1 0

**方法:**思路是使用[递归](https://www.geeksforgeeks.org/recursion/)的方式，不断再次调用同一个函数，直到 **N** 大于 **0** 并不断添加术语，之后开始打印术语。

按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **fibo(int N，int a，int b)** 其中
    *   **N** 是项的个数和
    *   **a** 和 **b** 为初始值，数值为 **0** 和 **1** 。
*   如果 **N** 大于 **0，**则再次调用该函数，值为 **N-1，b，a+b** 。
*   函数调用后，打印 **a** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the fibonacci
// series in reverse order.
void fibo(int n, int a, int b)
{
    if (n > 0) {

        // Function call
        fibo(n - 1, b, a + b);

        // Print the result
        cout << a << " ";
    }
}

// Driver Code
int main()
{
    int N = 10;
    fibo(N, 0, 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
// Function to print the fibonacci
// series in reverse order.
static void fibo(int n, int a, int b)
{
    if (n > 0) {

        // Function call
        fibo(n - 1, b, a + b);

        // Print the result
        System.out.print(a + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 10;
    fibo(N, 0, 1);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the fibonacci
# series in reverse order.
def fibo(n, a, b):

    if (n > 0):

        # Function call
        fibo(n - 1, b, a + b)

        # Print the result
        print(a, end=" ")

# Driver Code
if __name__ == "__main__":

    N = 10
    fibo(N, 0, 1)

    # This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
// Function to print the fibonacci
// series in reverse order.
static void fibo(int n, int a, int b)
{
    if (n > 0) {

        // Function call
        fibo(n - 1, b, a + b);

        // Print the result
        Console.Write(a + " ");
    }
}

// Driver Code
public static void Main()
{
    int N = 10;
    fibo(N, 0, 1);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the fibonacci
// series in reverse order.
function fibo(n, a, b)
{
    if (n > 0) {

        // Function call
        fibo(n - 1, b, a + b);

        // Print the result
        document.write(a + " ");
    }
}

// Driver Code
let N = 10;
fibo(N, 0, 1);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
34 21 13 8 5 3 2 1 1 0 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)