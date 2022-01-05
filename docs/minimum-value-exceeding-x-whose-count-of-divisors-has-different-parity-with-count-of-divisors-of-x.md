# 除数与 X 的除数不同的超过 X 的最小值

> 原文:[https://www . geesforgeks . org/最小值超出-x-谁的除数与-x 的除数具有不同的奇偶性/](https://www.geeksforgeeks.org/minimum-value-exceeding-x-whose-count-of-divisors-has-different-parity-with-count-of-divisors-of-x/)

给定一个整数 **X** ，任务是确定大于 **X** 的 **Y** 的最小值，使得 **X** 和 **Y** 的[除数](https://www.geeksforgeeks.org/count-divisors-n-on13/)具有不同的[重围](https://www.geeksforgeeks.org/finding-the-parity-of-a-number-efficiently/)。

**示例:**

> **输入:** X = 5
> **输出:** 9
> **说明:**5 和 9 的除数分别为 2 和 3，两者的 parities 不同。
> 
> **输入:** X = 9
> **输出:** 10
> **说明:**9 和 10 的除数分别为 3 和 4，它们的重围不同。

**天真法:**解决问题最简单的方法是从 **X + 1** 开始迭代每个数，直到得到一个除数与[奇偶性](https://www.geeksforgeeks.org/finding-the-parity-of-a-number-efficiently/)相反的元素 **X** 。

***时间复杂度:**O((1+√X)<sup>2</sup>)*
***辅助空间:** O(1)*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count divisors of n
int divisorCount(int n)
{
    int x = 0;
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            if (i == n / i)
                x++;
            else
                x += 2;
        }
    }
    return x;
}

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
int minvalue_y(int x)
{
    // Divisor count of x
    int a = divisorCount(x);
    int y = x + 1;

    // Iterate from x + 1 and
    // check for each element
    while ((a & 1)
           == (divisorCount(y) & 1))
        y++;
    return y;
}

// Driver Code
int main()
{
    // Given X
    int x = 5;

    // Function call
    cout << minvalue_y(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count divisors of n
static int divisorCount(int n)
{
    int x = 0;
    for(int i = 1; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (i == n / i)
                x++;
            else
                x += 2;
        }
    }
    return x;
}

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
static int minvalue_y(int x)
{

    // Divisor count of x
    int a = divisorCount(x);
    int y = x + 1;

    // Iterate from x + 1 and
    // check for each element
    while ((a & 1) == (divisorCount(y) & 1))
        y++;

    return y;
}

// Driver Code
public static void main(String[] args)
{

    // Given X
    int x = 5;

    // Function call
    System.out.println(minvalue_y(x));
}
}

// This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count divisors of n
static int divisorCount(int n)
{
    int x = 0;
    for(int i = 1; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (i == n / i)
                x++;
            else
                x += 2;
        }
    }
    return x;
}

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
static int minvalue_y(int x)
{

    // Divisor count of x
    int a = divisorCount(x);
    int y = x + 1;

    // Iterate from x + 1 and
    // check for each element
    while ((a & 1) == (divisorCount(y) & 1))
        y++;

    return y;
}

// Driver Code
public static void Main()
{

    // Given X
    int x = 5;

    // Function call
    Console.WriteLine(minvalue_y(x));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count divisors of n
def divisorCount(n):
    x = 0;
    for i in range(1, n):
        if (n % i == 0):
            if (i == n // i):
                x += 1;
            else:
                x += 2;
        if(i * i > n):
            break;

    return x;

# Function to find the minimum
# value exceeding x whose count
# of divisors has different parity
# with count of divisors of X
def minvalue_y(x):

    # Divisor count of x
    a = divisorCount(x);
    y = x + 1;

    # Iterate from x + 1 and
    # check for each element
    while ((a & 1) == (divisorCount(y) & 1)):
        y += 1;

    return y;

# Driver Code
if __name__ == '__main__':

    # Given X
    x = 5;

    # Function call
    print(minvalue_y(x));

# This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program of the above approach

// Function to count divisors of n
function divisorCount(n)
{
    let x = 0;
    for(let i = 1; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (i == n / i)
                x++;
            else
                x += 2;
        }
    }
    return x;
}

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
function minvalue_y(x)
{

    // Divisor count of x
    let a = divisorCount(x);
    let y = x + 1;

    // Iterate from x + 1 and
    // check for each element
    while ((a & 1) == (divisorCount(y) & 1))
        y++;

    return y;
}

    // Driver Code

     // Given X
    let x = 5;

    // Function call
    document.write(minvalue_y(x));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
9
```

**有效方法:**可以根据以下观察结果解决问题:

*   [如果 **X** 是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，那么 **X + 1** 就是答案。
*   否则**(1+√X)<sup>2</sup>T3 将是答案。**

按照以下步骤解决问题:

1.  [检查 **X** 是否是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果发现是真的，打印 **X + 1** 。
2.  否则，打印 **(1 +楼层(√X)) <sup>2</sup> )** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
int minvalue_y(int x)
{
    // Check if x is
    // perfect square
    int n = sqrt(x);
    if (n * n == x)
        return x + 1;

    return pow(n + 1, 2);
}

// Driver Code
int main()
{
    int x = 5;
    cout << minvalue_y(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
static int minvalue_y(int x)
{

    // Check if x is
    // perfect square
    int n = (int)Math.sqrt(x);
    if (n * n == x)
        return x + 1;

    return (int)Math.pow(n + 1, 2);
}

// Driver Code
public static void main(String[] args)
{
    int x = 5;

    System.out.print(minvalue_y(x));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# value exceeding x whose count
# of divisors has different parity
# with count of divisors of X
def minvalue_y(x):

    # Check if x is
    # perfect square
    n = int(pow(x, 1 / 2))

    if (n * n == x):
        return x + 1

    return(pow(n + 1, 2))

# Driver Code
if __name__ == '__main__':

    x = 5

    print(minvalue_y(x))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
static int minvalue_y(int x)
{

    // Check if x is
    // perfect square
    int n = (int)Math.Sqrt(x);
    if (n * n == x)
        return x + 1;

    return (int)Math.Pow(n + 1, 2);
}

// Driver Code
public static void Main()
{
    int x = 5;

    Console.WriteLine(minvalue_y(x));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum
// value exceeding x whose count
// of divisors has different parity
// with count of divisors of X
function minvalue_y(x)
{

    // Check if x is
    // perfect square
    let n = Math.floor(Math.sqrt(x));
    if (n * n == x)
        return x + 1;

    return Math.floor(Math.pow(n + 1, 2));
}

// Driver code

    let x = 5;

    document.write(minvalue_y(x));

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)