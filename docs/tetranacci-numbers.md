# 粉防己编号

> 原文:[https://www.geeksforgeeks.org/tetranacci-numbers/](https://www.geeksforgeeks.org/tetranacci-numbers/)

四纳奇数是由递归关系定义的斐波那契数的推广

> **T(n)= T(n-1)+T(n-2)+T(n-3)+T(n-4)**
> 同 **T(0)=0，T(1)=1，T(2)=1，T(3)=2，**

对于 n>=4。它们代表斐波那契 n 步数的 n=4 情况。n=0，1，…的前几个项是 0，1，1，2，4，8，15，29，56，108，208，…
给定一个数 N，任务是找到第 N 个四 acci 数。

**示例**:

```
Input: 5
Output: 4

Input: 9
Output: 108 
```

## [推荐:请先在 ***<u>{IDE}</u>*** 上尝试您的方法，然后再进入解决方案。](https://ide.geeksforgeeks.org/)

一种**天真的方法**是遵循递归来寻找数字，并使用递归来求解。
以下是上述办法的实施情况。

## C++

```
// A simple recursive CPP program to print
// the nth tetranacci numbers.
#include <iostream>
using namespace std;

// Function to return the
// N-th tetranacci number
int printTetraRec(int n)
{
    // base cases
    if (n == 0)
        return 0;
    // base cases
    if (n == 1 || n == 2)
        return 1;
    // base cases
    if (n == 3)
        return 2;

    else
        return printTetraRec(n - 1) + printTetraRec(n - 2)
               + printTetraRec(n - 3) + printTetraRec(n - 4);
}

// function to print the nth tetranacci number
void printTetra(int n)
{
    cout << printTetraRec(n) << " ";
}

// Driver code
int main()
{
    int n = 10;
    printTetra(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive Java
// program to print the nth
// tetranacci numbers.
class GFG
{
// Function to return the
// N-th tetranacci number
static int printTetraRec(int n)
{
    // base cases
    if (n == 0)
        return 0;
    // base cases
    if (n == 1 || n == 2)
        return 1;
    // base cases
    if (n == 3)
        return 2;

    else
        return printTetraRec(n - 1) +
               printTetraRec(n - 2) +
               printTetraRec(n - 3) +
               printTetraRec(n - 4);
}

// function to print the
// Nth tetranacci number
static void printTetra(int n)
{
    System.out.println(printTetraRec(n) + " ");
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    printTetra(n);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# A simple recursive Python3 program
# to print the nth tetranacci numbers.

# Function to return the
# N-th tetranacci number
def printTetraRec(n):

    # base cases
    if (n == 0):
        return 0;

    # base cases
    if (n == 1 or n == 2):
        return 1;

    # base cases
    if (n == 3):
        return 2;

    else:
        return (printTetraRec(n - 1) +
                printTetraRec(n - 2) +
                printTetraRec(n - 3) +
                printTetraRec(n - 4));

# function to print the
# nth tetranacci number
def printTetra(n):
    print(printTetraRec(n), end = " ");

# Driver code
n = 10;
printTetra(n);

# This code is contributed
# by mits
```

## C#

```
// A simple recursive C#
// program to print the nth
// tetranacci numbers.
class GFG
{

// Function to return the
// N-th tetranacci number
static int printTetraRec(int n)
{
    // base cases
    if (n == 0)
        return 0;
    // base cases
    if (n == 1 || n == 2)
        return 1;
    // base cases
    if (n == 3)
        return 2;

    else
        return printTetraRec(n - 1) +
               printTetraRec(n - 2) +
               printTetraRec(n - 3) +
               printTetraRec(n - 4);
}

// function to print the
// Nth tetranacci number
static void printTetra(int n)
{
    System.Console.WriteLine(
           printTetraRec(n) + " ");
}

// Driver code
static void Main()
{
    int n = 10;
    printTetra(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple recursive PHP program
// to print the nth tetranacci numbers.

// Function to return the
// N-th tetranacci number
function printTetraRec($n)
{
    // base cases
    if ($n == 0)
        return 0;

    // base cases
    if ($n == 1 || $n == 2)
        return 1;

    // base cases
    if ($n == 3)
        return 2;

    else
        return printTetraRec($n - 1) +
               printTetraRec($n - 2) +
               printTetraRec($n - 3) +
               printTetraRec($n - 4);
}

// function to print the
// nth tetranacci number
function printTetra($n)
{
    echo printTetraRec($n) . " ";
}

// Driver code
$n = 10;
printTetra($n);

// This code is contributed
// by Abby_akku
?>
```

## java 描述语言

```
<script>

    // A simple recursive Javascript
    // program to print the nth
    // tetranacci numbers.

    // Function to return the
    // N-th tetranacci number
    function printTetraRec(n)
    {
        // base cases
        if (n == 0)
            return 0;
        // base cases
        if (n == 1 || n == 2)
            return 1;
        // base cases
        if (n == 3)
            return 2;

        else
            return printTetraRec(n - 1) +
                   printTetraRec(n - 2) +
                   printTetraRec(n - 3) +
                   printTetraRec(n - 4);
    }

    // function to print the
    // Nth tetranacci number
    function printTetra(n)
    {
        document.write(printTetraRec(n) + " " + "</br>");
    }

    let n = 10;
    printTetra(n);

</script>
```

**Output:** 

```
208
```

**时间复杂度:** O(4 <sup>N</sup> )

一个**更好的解决方案**是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)(记忆化)，因为有多个重叠。
下面给出的是 N=10 的递归树。

```
                                        rec(10)

                             /         /       \          \

                       rec(9)      rec(8)     rec(7)     rec(6)

              /      /     \     \

          rec(8) rec(7)  rec(6)  rec(5)
```

在上面的部分递归树中，rec(8)、rec(7)、rec(6)已经被求解了两次。在绘制完整的递归树时，已经观察到有许多子问题被反复解决。因此，该问题具有重叠子结构性质，用记忆法或制表法都可以避免同一子问题的重新计算。
以下是上述办法的实施情况。

## C++

```
// A DP based CPP
// program to print
// the nth tetranacci number
#include <iostream>
using namespace std;

// Function to print the
// N-th tetranacci number
int printTetra(int n)
{
    int dp[n + 5];
    // base cases
    dp[0] = 0;
    dp[1] = dp[2] = 1;
    dp[3] = 2;

    for (int i = 4; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2] +
                dp[i - 3] + dp[i - 4];

    cout << dp[n];
}

// Driver code
int main()
{
    int n = 10;
    printTetra(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A DP based Java
// program to print
// the nth tetranacci number

class GFG{
// Function to print the
// N-th tetranacci number
static void printTetra(int n)
{
    int[] dp=new int[n + 5];
    // base cases
    dp[0] = 0;
    dp[1] = dp[2] = 1;
    dp[3] = 2;

    for (int i = 4; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2] +
                dp[i - 3] + dp[i - 4];

    System.out.print(dp[n]);
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    printTetra(n);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# A DP based Python3 program to print
# the nth tetranacci number

# Function to print the
# N-th tetranacci number
def printTetra(n):
    dp = [0] * (n + 5);

    # base cases
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 1;
    dp[3] = 2;

    for i in range(4, n + 1):
        dp[i] = (dp[i - 1] + dp[i - 2] +
                 dp[i - 3] + dp[i - 4]);

    print(dp[n]);

# Driver code
n = 10;
printTetra(n);

# This code is contributed by mits
```

## C#

```
// A DP based C#
// program to print
// the nth tetranacci number

class GFG{
// Function to print the
// N-th tetranacci number
static void printTetra(int n)
{
    int[] dp=new int[n + 5];
    // base cases
    dp[0] = 0;
    dp[1] = dp[2] = 1;
    dp[3] = 2;

    for (int i = 4; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2] +
                dp[i - 3] + dp[i - 4];

    System.Console.WriteLine(dp[n]);
}

// Driver code
static void Main()
{
    int n = 10;
    printTetra(n);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A DP based PHP
// program to print
// the nth tetranacci number

// Function to print the
// N-th tetranacci number
function printTetra($n)
{
    $dp = array_fill(0, $n + 5, 0);

    // base cases
    $dp[0] = 0;
    $dp[1] = $dp[2] = 1;
    $dp[3] = 2;

    for ($i = 4; $i <= $n; $i++)
        $dp[$i] = $dp[$i - 1] + $dp[$i - 2] +
                  $dp[$i - 3] + $dp[$i - 4];

    echo $dp[$n];
}

// Driver code
$n = 10;
printTetra($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // A DP based Javascript
    // program to print
    // the nth tetranacci number

    // Function to print the
    // N-th tetranacci number
    function printTetra(n)
    {
        let dp=new Array(n + 5);
        // base cases
        dp[0] = 0;
        dp[1] = dp[2] = 1;
        dp[3] = 2;

        for (let i = 4; i <= n; i++)
            dp[i] = dp[i - 1] + dp[i - 2] +
                    dp[i - 3] + dp[i - 4];

        document.write(dp[n]);
    }

    let n = 10;
    printTetra(n);

</script>
```

**Output:** 

```
208
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

上面的时间复杂度是线性的，但是需要额外的空间。在上面的解决方案中，通过使用四个变量来跟踪前四个数字，可以优化使用的空间。
以下是上述办法的实施情况。

## C++

```
// A space optimized
// based CPP program to
// print the nth tetranacci number
#include <iostream>
using namespace std;

// Function to print the
// N-th tetranacci number
void printTetra(int n)
{
    if (n < 0)
        return;

    // Initialize first
    // four numbers to base cases
    int first = 0, second = 1;
    int third = 1, fourth = 2;

    // declare a current variable
    int curr;

    if (n == 0)
        cout << first;
    else if (n == 1 || n == 2)
        cout << second;

    else if (n == 3)
        cout << fourth;

    else {

        // Loop to add previous
        // four numbers for
        // each number starting
        // from 4 and then assign
        // first, second, third
        // to second, third, fourth and
        // curr to fourth respectively
        for (int i = 4; i <= n; i++) {
            curr = first + second + third + fourth;
            first = second;
            second = third;
            third = fourth;
            fourth = curr;
        }
        cout << curr;
    }
}

// Driver code
int main()
{
    int n = 10;
    printTetra(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A space optimized
// based Java program to
// print the nth tetranacci number
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG{
// Function to print the
// N-th tetranacci number
static void printTetra(int n)
{
    if (n < 0)
        return;

    // Initialize first
    // four numbers to base cases
    int first = 0, second = 1;
    int third = 1, fourth = 2;

    // declare a current variable
    int curr = 0;

    if (n == 0)
        System.out.print(first);
    else if (n == 1 || n == 2)
        System.out.print(second);

    else if (n == 3)
        System.out.print(fourth);

    else
    {

        // Loop to add previous
        // four numbers for
        // each number starting
        // from 4 and then assign
        // first, second, third
        // to second, third, fourth and
        // curr to fourth respectively
        for (int i = 4; i <= n; i++)
        {
            curr = first + second + third + fourth;
            first = second;
            second = third;
            third = fourth;
            fourth = curr;
        }
        System.out.print(curr);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    printTetra(n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# A space optimized based Python3 program
# to print the nth tetranacci number

# Function to print the N-th
# tetranacci number
def printTetra(n):

    if (n < 0):
        return;

    # Initialize first four
    # numbers to base cases
    first = 0;
    second = 1;
    third = 1;
    fourth = 2;

    # declare a current variable
    curr = 0;

    if (n == 0):
        print(first);
    elif (n == 1 or n == 2):
        print(second);

    elif (n == 3):
        print(fourth);

    else:

        # Loop to add previous four numbers
        # for each number starting from 4
        # and then assign first, second,
        # third to second, third, fourth
        # and curr to fourth respectively
        for i in range(4, n + 1):
            curr = first + second + third + fourth;
            first = second;
            second = third;
            third = fourth;
            fourth = curr;

    print(curr);

# Driver code
n = 10;
printTetra(n);

# This code is contributed by mits
```

## C#

```
// A space optimized based C# program to
// print the nth tetranacci number
using System;

class GFG{

// Function to print the
// N-th tetranacci number
static void printTetra(int n)
{
    if (n < 0)
        return;

    // Initialize first
    // four numbers to base cases
    int first = 0, second = 1;
    int third = 1, fourth = 2;

    // declare a current variable
    int curr = 0;

    if (n == 0)
        Console.Write(first);
    else if (n == 1 || n == 2)
        Console.Write(second);

    else if (n == 3)
        Console.Write(fourth);

    else
    {

        // Loop to add previous
        // four numbers for
        // each number starting
        // from 4 and then assign
        // first, second, third
        // to second, third, fourth and
        // curr to fourth respectively
        for (int i = 4; i <= n; i++)
        {
            curr = first + second + third + fourth;
            first = second;
            second = third;
            third = fourth;
            fourth = curr;
        }
        Console.Write(curr);
    }
}

    // Driver code
    static public void Main ()
    {

        int n = 10;
        printTetra(n);
    }
}

// This code is contributed ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A space optimized based PHP program
// to print the nth tetranacci number

// Function to print the N-th
// tetranacci number

function printTetra($n)
{
    if ($n < 0)
        return;

    // Initialize first four
    // numbers to base cases
    $first = 0;
    $second = 1;
    $third = 1;
    $fourth = 2;

    // declare a current variable
    $curr;

    if ($n == 0)
        echo $first;
    else if ($n == 1 || $n == 2)
        echo $second;

    else if ($n == 3)
        echo $fourth;

    else
    {

        // Loop to add previous four
        // numbers for each number
        // starting from 4 and then
        // assign first, second, third
        // to second, third, fourth and
        // curr to fourth respectively
        for ($i = 4; $i <= $n; $i++)
        {
            $curr = $first + $second +
                    $third + $fourth;
            $first = $second;
            $second = $third;
            $third = $fourth;
            $fourth = $curr;
        }
    echo $curr;
    }
}

// Driver code
$n = 10;
printTetra($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// A space optimized
// based Javascript program to
// print the nth tetranacci number

// Function to print the
// N-th tetranacci number
function printTetra(n)
{
    if (n < 0)
        return;

    // Initialize first
    // four numbers to base cases
    var first = 0, second = 1;
    var third = 1, fourth = 2;

    // declare a current variable
    var curr;

    if (n == 0)
        cout << first;
    else if (n == 1 || n == 2)
        cout << second;

    else if (n == 3)
        cout << fourth;

    else {

        // Loop to add previous
        // four numbers for
        // each number starting
        // from 4 and then assign
        // first, second, third
        // to second, third, fourth and
        // curr to fourth respectively
        for (var i = 4; i <= n; i++) {
            curr = first + second + third + fourth;
            first = second;
            second = third;
            third = fourth;
            fourth = curr;
        }
        document.write( curr);
    }
}

// Driver code
var n = 10;
printTetra(n);

</script>
```

**Output:** 

```
208
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)