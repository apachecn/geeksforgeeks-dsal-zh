# Golomb 序列

> 原文:[https://www.geeksforgeeks.org/golomb-sequence/](https://www.geeksforgeeks.org/golomb-sequence/)

在数学中， **Golomb 序列**是一个非递减的整数序列，其中第 n 项等于 n 在序列中出现的次数。
前几个数值是
1，2，2，3，3，4，4，4，5，5，5，…

几个术语的解释:
第三个术语是 2，注意三个出现 2 次。
第二项为 2，注意两个出现 2 次。
第四任是 3，注意 4 出现 3 次。
给定正整数 n，任务是求 Golomb 序列的前 n 项。

**示例:**

```
Input : n = 4
Output : 1 2 2 3

Input : n = 6
Output : 1 2 2 3 3 4
```

求 Golomb 序列第 n 项的递推关系:
a(1)= 1
a(n+1)= 1+a(n+1–a(a(n)))

下面是使用递归的实现:

## C++

```
// C++ Program to find first
// n terms of Golomb sequence.
#include <bits/stdc++.h>
using namespace std;

// Return the nth element
// of Golomb sequence
int findGolomb(int n)
{
    // base case
    if (n == 1)
        return 1;

    // Recursive Step
    return 1 + findGolomb(n -
               findGolomb(findGolomb(n - 1)));
}

// Print the first n
// term of Golomb Sequence
void printGolomb(int n)
{
    // Finding first n
    // terms of Golomb Sequence.
    for (int i = 1; i <= n; i++)
        cout << findGolomb(i) << " ";
}

// Driver Code
int main()
{
    int n = 9;
    printGolomb(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find first 
// n terms of Golomb sequence.
import java.util.*;

class GFG
{
    public static int findGolomb(int n)
    {

        // base case
        if (n == 1)
            return 1;

        // Recursive Step
        return 1 + findGolomb(n -
        findGolomb(findGolomb(n - 1)));
    }

    // Print the first n term of
    // Golomb Sequence
    public static void printGolomb(int n)
    {

        // Finding first n terms of
        // Golomb Sequence.
        for (int i = 1; i <= n; i++)
            System.out.print(findGolomb(i) +
                                       " ");
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 9;

        printGolomb(n);
    }
}

// This code is contributed by Akash Singh
```

## 蟒蛇 3

```
# Python 3 Program to find first
# n terms of Golomb sequence.

# Return the nth element of
# Golomb sequence
def findGolomb(n):

    # base case
    if (n == 1):
        return 1

    # Recursive Step
    return 1 + findGolomb(n -
    findGolomb(findGolomb(n - 1)))

# Print the first n term
# of Golomb Sequence
def printGolomb(n):

    # Finding first n terms of
    # Golomb Sequence.
    for i in range(1, n + 1):
        print(findGolomb(i), end=" ")

# Driver Code
n = 9

printGolomb(n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to find first n 
// terms of Golomb sequence.
using System;

class GFG
{

    // Return the nth element
    // of Golomb sequence
    static int findGolomb(int n)
    {

        // base case
        if (n == 1)
            return 1;

        // Recursive Step
        return 1 + findGolomb(n -
        findGolomb(findGolomb(n - 1)));
    }

    // Print the first n term 
    // of Golomb Sequence
    static void printGolomb(int n)
    {
        // Finding first n terms of
        // Golomb Sequence.
        for (int i = 1; i <= n; i++)
            Console .Write(findGolomb(i) +
                                     " ");
    }

    // Driver Code
    public static void Main ()
    {

        int n = 9;

        printGolomb(n);

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find first
// n terms of Golomb sequence.

// Return the nth element
// of Golomb sequence
function findGolomb($n)
{

    // base case
    if ($n == 1)
        return 1;

    // Recursive Step
    return 1 + findGolomb($n -
        findGolomb(findGolomb($n - 1)));
}

// Print the first n
// term of Golomb Sequence
function printGolomb($n)
{

    // Finding first n terms
    // of Golomb Sequence.
    for ($i = 1; $i <= $n; $i++)
        echo findGolomb($i) , " ";
}

// Driver Code
$n = 9;
printGolomb($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript Program to find first 
// n terms of Golomb sequence.

    function findGolomb(n)
    {

        // base case
        if (n == 1)
            return 1;

        // Recursive Step
        return 1 + findGolomb(n - findGolomb(findGolomb(n - 1)));
    }

    // Print the first n term of
    // Golomb Sequence
    function printGolomb(n)
    {

        // Finding first n terms of
        // Golomb Sequence.
        for (let i = 1; i <= n; i++)
            document.write(findGolomb(i) + " ");
    }

    // Driver Code   
    var n = 9;
    printGolomb(n);

// This code is contributed by Amit Katiyar
</script>
```

**Output :** 

```
1 2 2 3 3 4 4 4 5
```

下面是使用动态编程的实现:

## C++

```
// C++ Program to find first
// n terms of Golomb sequence.
#include <bits/stdc++.h>
using namespace std;

// Print the first n term
// of Golomb Sequence
void printGolomb(int n)
{
    int dp[n + 1];

    // base cases
    dp[1] = 1;
    cout << dp[1] << " ";

    // Finding and printing first
    // n terms of Golomb Sequence.
    for (int i = 2; i <= n; i++)
    {
        dp[i] = 1 + dp[i - dp[dp[i - 1]]];
        cout << dp[i] << " ";
    }
}
// Driver Code
int main()
{
    int n = 9;

    printGolomb(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find first
// n terms of Golomb sequence.
import java.util.*;

class GFG
{

    public static void printGolomb(int n)
    {
        int dp[] = new int[n + 1];

        // base cases
        dp[1] = 1;
        System.out.print(dp[1] + " ");

        // Finding and printing first n
        // terms of Golomb Sequence.
        for (int i = 2; i <= n; i++)
        {
            dp[i] = 1 + dp[i - dp[dp[i - 1]]];

        System.out.print(dp[i] + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 9;

        printGolomb(n);
    }
}

// This code is contributed by Akash Singh
```

## 蟒蛇 3

```
# Python3 Program to find first
# n terms of Golomb sequence.

# Print the first n term
# of Golomb Sequence
def Golomb( n):

    dp = [0] * (n + 1)

    # base cases
    dp[1] = 1
    print(dp[1], end = " " )

    # Finding and pring first
    # n terms of Golomb Sequence.
    for i in range(2, n + 1):

        dp[i] = 1 + dp[i - dp[dp[i - 1]]]
        print(dp[i], end = " ")

# Driver Code
n = 9

Golomb(n)

# This code is contributed by ash264
```

## C#

```
// C# Program to find first n
// terms of Golomb sequence.
using System;

class GFG
{

    // Print the first n term of
    // Golomb Sequence
    static void printGolomb(int n)
    {
        int []dp = new int[n + 1];

        // base cases
        dp[1] = 1;
        Console.Write(dp[1] + " ");

        // Finding and printing first n
        // terms of Golomb Sequence.
        for (int i = 2; i <= n; i++)
        {
            dp[i] = 1 + dp[i - dp[dp[i - 1]]];
            Console.Write( dp[i] + " ");
        }
    }

    // Driver Code
    public static void Main ()
    {

        int n = 9;

        printGolomb(n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find first
// n terms of Golomb sequence.

// Print the first n term
// of Golomb Sequence
function printGolomb($n)
{
    // base cases
    $dp[1] = 1;
    echo $dp[1], " ";

    // Finding and printing first
    // n terms of Golomb Sequence.
    for ($i = 2; $i <= $n; $i++)
    {
        $dp[$i] = 1 + $dp[$i -
                          $dp[$dp[$i - 1]]];
        echo $dp[$i], " ";
    }
}
// Driver Code
$n = 9;

printGolomb($n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Javascript Program to find first
// n terms of Golomb sequence.

// Print the first n term
// of Golomb Sequence
     function printGolomb( n) {
        let dp = Array(n + 1).fill(0);

        // base cases
        dp[1] = 1;
        document.write(dp[1] + " ");

        // Finding and printing first n
        // terms of Golomb Sequence.
        for ( i = 2; i <= n; i++) {
            dp[i] = 1 + dp[i - dp[dp[i - 1]]];

            document.write(dp[i] + " ");
        }
    }

    // Driver code

        let n = 9;

        printGolomb(n);

// This code is contributed by shikhasingrajput

</script>
```

**Output :** 

```
1 2 2 3 3 4 4 4 5
```