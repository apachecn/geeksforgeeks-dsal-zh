# 求除 X 和 Y 的数，得到相同的余数

> 原文:[https://www . geesforgeks . org/find-numbers-将 x 和 y 相除以产生相同的余数/](https://www.geeksforgeeks.org/find-numbers-that-divide-x-and-y-to-produce-the-same-remainder/)

给定两个整数 **X** 和 **Y** ，任务是找到并打印将 X 和 Y 除的数字，以产生相同的余数。
**例:**

> **输入:** X = 1，Y = 5
> **输出:** 1，2，4
> **说明:**
> 让数字为 M，可以是[1，5]:
> 范围内的任意值如果 M = 1，1 % 1 = 0 和 5 % 1 = 0
> 如果 M = 2，1 % 2 = 1 和 5 % 2 = 1
> 如果 M = 3， 1 % 3 = 1 和 5 % 3 = 2
> 如果 M = 4，1 % 4 = 1 和 5 % 4 = 1
> 如果 M = 5，1 % 5 = 1 和 5 % 5 = 0
> 因此，可能的 M 值为 1，2，4
> **输入:** X = 8，Y = 10
> **输出:** 1，2

**天真法:**这个问题的天真法是检查[1，max(X，Y)]范围内 M 的所有可能值的模值，如果条件满足则打印 M 的值。
以下是上述办法的实施情况:

## C++

```
// C++ program to find numbers
// that divide X and Y
// to produce the same remainder

#include <iostream>
using namespace std;

// Function to find
// the required number as M
void printModulus(int X, int Y)
{
    // Finding the maximum
    // value among X and Y
    int n = max(X, Y);

    // Loop to iterate through
    // maximum value among X and Y.
    for (int i = 1; i <= n; i++) {

        // If the condition satisfies, then
        // print the value of M
        if (X % i == Y % i)
            cout << i << " ";
    }
}

// Driver code
int main()
{

    int X, Y;
    X = 10;
    Y = 20;
    printModulus(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find numbers
// that divide X and Y
// to produce the same remainder
class GFG{

// Function to find
// the required number as M
static void printModulus(int X, int Y)
{
    // Finding the maximum
    // value among X and Y
    int n = Math.max(X, Y);

    // Loop to iterate through
    // maximum value among X and Y.
    for (int i = 1; i <= n; i++) {

        // If the condition satisfies, then
        // print the value of M
        if (X % i == Y % i)
            System.out.print(i + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    int X, Y;
    X = 10;
    Y = 20;
    printModulus(X, Y);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program to find numbers
# that divide X and Y
# to produce the same remainder

# Function to find
# the required number as M
def printModulus( X, Y):

    # Finding the maximum
    # value among X and Y
    n = max(X, Y)

    # Loop to iterate through
    # maximum value among X and Y.
    for i in range(1, n + 1):

        # If the condition satisfies, then
        # print the value of M
        if (X % i == Y % i):
            print(i,end=" ")

# Driver code
X = 10
Y = 20
printModulus(X, Y)

# This code is contributed by Atul_kumar_Shrivastava
```

## C#

```
// C# program to find numbers
// that divide X and Y
// to produce the same remainder
using System;

class GFG{

// Function to find
// the required number as M
static void printModulus(int X, int Y)
{
    // Finding the maximum
    // value among X and Y
    int n = Math.Max(X, Y);

    // Loop to iterate through
    // maximum value among X and Y.
    for (int i = 1; i <= n; i++) {

        // If the condition satisfies, then
        // print the value of M
        if (X % i == Y % i)
            Console.Write(i + " ");
    }
}

// Driver code
public static void Main()
{
    int X, Y;
    X = 10;
    Y = 20;
    printModulus(X, Y);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// Javascript program to find numbers
// that divide X and Y
// to produce the same remainder

// Function to find
// the required number as M
function printModulus(X, Y)
{
    // Finding the maximum
    // value among X and Y
    var n = Math.max(X, Y);

    // Loop to iterate through
    // maximum value among X and Y.
    for (var i = 1; i <= n; i++) {

        // If the condition satisfies, then
        // print the value of M
        if (X % i == Y % i)
            document.write(i+" ");
    }
}

// Driver code
X = 10;
Y = 20;
printModulus(X, Y);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1 2 5 10
```

***时间复杂度:** O(max(X，Y))*

***辅助空间:** O(1)*
**高效进场:**我们假设 **Y** 比 **X** 大 **D** 的差。

*   那么 **Y** 可以表示为

```
Y = X + D
and
Y % M = (X + D) % M
      = (X % M) + (D % M)
```

*   现在，条件变成**X % M 和 X % M + D % M 是否相等**。
*   这里，由于 X % M 在两边都很常见，如果对于某些 M， **D % M = 0** ，则 M 的值为真。
*   因此，M 的要求值将是 D 的**因子。**

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find numbers
// that divide X and Y to
// produce the same remainder

#include <iostream>
using namespace std;

// Function to print all the possible values
// of M such that X % M = Y % M
void printModulus(int X, int Y)
{
    // Finding the absolute difference
    // of X and Y
    int d = abs(X - Y);

    // Iterating from 1
    int i = 1;

    // Loop to print all the factors of D
    while (i * i <= d) {

        // If i is a factor of d, then print i
        if (d % i == 0) {
            cout << i << " ";

            // If d / i is a factor of d,
            // then print d / i
            if (d / i != i)
                cout << d / i << " ";
        }
        i++;
    }
}

// Driver code
int main()
{

    int X = 10;
    int Y = 26;

    printModulus(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find numbers
// that divide X and Y to
// produce the same remainder
import java.util.*;

class GFG{

// Function to print all the possible values
// of M such that X % M = Y % M
static void printModulus(int X, int Y)
{
    // Finding the absolute difference
    // of X and Y
    int d = Math.abs(X - Y);

    // Iterating from 1
    int i = 1;

    // Loop to print all the factors of D
    while (i * i <= d) {

        // If i is a factor of d, then print i
        if (d % i == 0) {
            System.out.print(i+ " ");

            // If d / i is a factor of d,
            // then print d / i
            if (d / i != i)
                System.out.print(d / i+ " ");
        }
        i++;
    }
}

// Driver code
public static void main(String[] args)
{

    int X = 10;
    int Y = 26;

    printModulus(X, Y);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program to find numbers
# that divide X and Y to
# produce the same remainder

# Function to prall the possible values
# of M such that X % M = Y % M
def printModulus(X, Y):
    # Finding the absolute difference
    # of X and Y
    d = abs(X - Y);

    # Iterating from 1
    i = 1;

    # Loop to prall the factors of D
    while (i * i <= d):

        # If i is a factor of d, then pri
        if (d % i == 0):
            print(i, end="");

            # If d / i is a factor of d,
            # then prd / i
            if (d // i != i):
                print(d // i, end=" ");

        i+=1;

# Driver code
if __name__ == '__main__':

    X = 10;
    Y = 26;

    printModulus(X, Y);

# This code contributed by Princi Singh
```

## C#

```
// C# program to find numbers
// that divide X and Y to
// produce the same remainder
using System;

public class GFG{

// Function to print all the possible values
// of M such that X % M = Y % M
static void printModulus(int X, int Y)
{
    // Finding the absolute difference
    // of X and Y
    int d = Math.Abs(X - Y);

    // Iterating from 1
    int i = 1;

    // Loop to print all the factors of D
    while (i * i <= d) {

        // If i is a factor of d, then print i
        if (d % i == 0) {
            Console.Write(i+ " ");

            // If d / i is a factor of d,
            // then print d / i
            if (d / i != i)
                Console.Write(d / i+ " ");
        }
        i++;
    }
}

// Driver code
public static void Main(String[] args)
{

    int X = 10;
    int Y = 26;

    printModulus(X, Y);
}
}

// This code contributed by Princi Singh
```

## java 描述语言

```
  <script>
    // Javascript program to find numbers
    // that divide X and Y to
    // produce the same remainder

    // Function to print all the possible values
    // of M such that X % M = Y % M
    function printModulus(X, Y)
    {

      // Finding the absolute difference
      // of X and Y
      var d = Math.abs(X - Y);

      // Iterating from 1
      var i = 1;

      // Loop to print all the factors of D
      while (i * i <= d) {

        // If i is a factor of d, then print i
        if (d % i == 0) {
          document.write(i + " ");

          // If d / i is a factor of d,
          // then print d / i
          if (d / i != i)
            document.write(parseInt(d / i) + " ");
        }
        i++;
      }
    }

    // Driver code
    var X = 10;
    var Y = 26;
    printModulus(X, Y);

// This code is contributed by rrrtnx.
  </script>
```

**Output:** 

```
1 16 2 8 4
```

***时间复杂度分析** O(sqrt(D))* ，其中 D 为 X 和 y 值之差

***辅助空间:**O(1)*T4】