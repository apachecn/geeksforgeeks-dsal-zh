# 打印给定范围内的所有完美方块

> 原文:[https://www . geesforgeks . org/print-all-perfect-squares-from-the-给定范围/](https://www.geeksforgeeks.org/print-all-perfect-squares-from-the-given-range/)

给定一个范围**【L，R】**，任务是打印给定范围内的所有完美方块。
**例:**

> **输入:** L = 2，R = 24
> **输出:** 4 9 16
> **输入:** L = 1，R = 100
> **输出:** 1 4 9 16 25 36 49 64 81 100

**天真的做法:**从 L 开始到 R 检查当前元素是否是完美的正方形。如果是，那么打印出来。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the perfect
// squares from the given range
void perfectSquares(float l, float r)
{

    // For every element from the range
    for (int i = l; i <= r; i++) {

        // If current element is
        // a perfect square
        if (sqrt(i) == (int)sqrt(i))
            cout << i << " ";
    }
}

// Driver code
int main()
{
    int l = 2, r = 24;

    perfectSquares(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.io.*;

class GFG
{

// Function to print all the perfect
// squares from the given range
static void perfectSquares(int l, int r)
{

    // For every element from the range
    for (int i = l; i <= r; i++)
    {

        // If current element is
        // a perfect square
        if (Math.sqrt(i) == (int)Math.sqrt(i))
            System.out.print(i + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    int l = 2, r = 24;
    perfectSquares(l, r);
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print all the perfect
# squares from the given range
def perfectSquares(l, r):

    # For every element from the range
    for i in range(l, r + 1):

        # If current element is
        # a perfect square
        if (i**(.5) == int(i**(.5))):
            print(i, end=" ")

# Driver code
l = 2
r = 24

perfectSquares(l, r)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print all the perfect
// squares from the given range
static void perfectSquares(int l, int r)
{

    // For every element from the range
    for (int i = l; i <= r; i++)
    {

        // If current element is
        // a perfect square
        if (Math.Sqrt(i) == (int)Math.Sqrt(i))
            Console.Write(i + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int l = 2, r = 24;
    perfectSquares(l, r);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// js implementation of the approach

// Function to print all the perfect
// squares from the given range
function perfectSquares(l, r){

    //For every element from the range
    for (let i = l; i <= r; i++)
    {

        // If current element is
        // a perfect square
        if (Math.sqrt(i) == parseInt(Math.sqrt(i)))
            document.write(i + " ");
    }
}

// Driver code
let l = 2;
let r = 24;
perfectSquares(l, r)

// This code is contributed by sravan.
</script>
```

**Output:** 

```
4 9 16
```

它是含氧(氮)的溶液。此外，平方根数量的使用导致计算费用。
**有效方法:**这种方法基于这样一个事实，即在数字 **L** 之后的第一个完美正方形肯定是 **⌈sqrt(L)⌉** 的正方形。简单来说 **L** 的平方根会非常接近我们要找的平方根的数字。因此，该数字将为 **pow(ceil(sqrt(L))，2)** 。
第一个完美的正方形对这个方法很重要。现在原来的答案就隐藏在这个图案上面即**0 1 4 9 16 25**
0 和 1 的差是 1
1 和 4 的差是 3
4 和 9 的差是 5 以此类推……
意思就是两个完美正方形的差总是奇数。
现在，问题来了，要得到下一个数字必须加上什么，答案是 **(sqrt(X) * 2) + 1** ，其中 **X** 是已知的完美正方形。
让当前完美方块为 **4** ，那么下一个完美方块肯定会是 **4 + (sqrt(4) * 2 + 1) = 9** 。这里加数 **5** ，下一个要加的数将是 **7** 然后是 **9** 以此类推……这样就组成了一系列奇数。
加法比执行乘法或求每个数的平方根计算成本低。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the perfect
// squares from the given range
void perfectSquares(float l, float r)
{

    // Getting the very first number
    int number = ceil(sqrt(l));

    // First number's square
    int n2 = number * number;

    // Next number is at the difference of
    number = (number * 2) + 1;

    // While the perfect squares
    // are from the range
    while ((n2 >= l && n2 <= r)) {

        // Print the perfect square
        cout << n2 << " ";

        // Get the next perfect square
        n2 = n2 + number;

        // Next odd number to be added
        number += 2;
    }
}

// Driver code
int main()
{
    int l = 2, r = 24;

    perfectSquares(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print all the perfect
// squares from the given range
static void perfectSquares(float l, float r)
{

    // Getting the very first number
    int number = (int) Math.ceil(Math.sqrt(l));

    // First number's square
    int n2 = number * number;

    // Next number is at the difference of
    number = (number * 2) + 1;

    // While the perfect squares
    // are from the range
    while ((n2 >= l && n2 <= r))
    {

        // Print the perfect square
        System.out.print(n2 + " ");

        // Get the next perfect square
        n2 = n2 + number;

        // Next odd number to be added
        number += 2;
    }
}

// Driver code
public static void main(String[] args)
{
    int l = 2, r = 24;

    perfectSquares(l, r);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

from math import ceil, sqrt

# Function to print all the perfect
# squares from the given range
def perfectSquares(l, r) :

    # Getting the very first number
    number = ceil(sqrt(l));

    # First number's square
    n2 = number * number;

    # Next number is at the difference of
    number = (number * 2) + 1;

    # While the perfect squares
    # are from the range
    while ((n2 >= l and n2 <= r)) :

        # Print the perfect square
        print(n2, end= " ");

        # Get the next perfect square
        n2 = n2 + number;

        # Next odd number to be added
        number += 2;

# Driver code
if __name__ == "__main__" :

    l = 2; r = 24;

    perfectSquares(l, r);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print all the perfect
// squares from the given range
static void perfectSquares(float l, float r)
{

    // Getting the very first number
    int number = (int) Math.Ceiling(Math.Sqrt(l));

    // First number's square
    int n2 = number * number;

    // Next number is at the difference of
    number = (number * 2) + 1;

    // While the perfect squares
    // are from the range
    while ((n2 >= l && n2 <= r))
    {

        // Print the perfect square
        Console.Write(n2 + " ");

        // Get the next perfect square
        n2 = n2 + number;

        // Next odd number to be added
        number += 2;
    }
}

// Driver code
public static void Main(String[] args)
{
    int l = 2, r = 24;

    perfectSquares(l, r);
}
}

// This code is contributed by Rajput Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to print all the perfect
// squares from the given range
function perfectSquares(l, r)
{

    // Getting the very first number
    let number = Math.ceil(Math.sqrt(l));

    // First number's square
    let n2 = number * number;

    // Next number is at the difference of
    number = (number * 2) + 1;

    // While the perfect squares
    // are from the range
    while ((n2 >= l && n2 <= r)) {

        // Print the perfect square
        document.write(n2 + " ");

        // Get the next perfect square
        n2 = n2 + number;

        // Next odd number to be added
        number += 2;
    }
}

// Driver code
let l = 2, r = 24;

perfectSquares(l, r);

// This code is contributed by subhammahato348
</script>
```

**Output:** 

```
4 9 16
```