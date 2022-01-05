# 使用递归求解 f(n)=(1)+(2 * 3)+(4 * 5 * 6)…n

> 原文:[https://www . geesforgeks . org/solution-fn-1-23-456-n-use-recursion/](https://www.geeksforgeeks.org/solving-fn-1-23-456-n-using-recursion/)

**例:**

```
Input : 2
Output: 7
Series: (1) + (2*3)

Input : 4
Output: 5167
Series: (1) + (2*3) + (4*5*6) + (7*8*9*10) 
```

## C++

```
// CPP Program to print the solution
// of the series f(n)= (1) + (2*3)
// + (4*5*6) ... n using recursion
#include<bits/stdc++.h>
using namespace std;

// Recursive function for
// finding sum of series
// calculated - number of terms till
//             which sum of terms has
//             been calculated
// current - number of terms for which
//             sum has to becalculated
// N         - Number of terms in the
//             function to be calculated
int seriesSum(int calculated, int current,
                            int N)
{
    int i, cur = 1;

    // checking termination condition
    if (current == N + 1)
        return 0;

    // product of terms till current
    for (i = calculated; i < calculated +
                            current; i++)
        cur *= i;

    // recursive call for adding
    // terms next in the series
    return cur + seriesSum(i, current + 1, N);
}

// Driver Code
int main()
{
    // input number of terms in the series
    int N = 5;

    // invoking the function to
    // calculate the sum
    cout<<seriesSum(1, 1, N)<<endl;

    return 0;
}
```

## C

```
// C Program to print the solution
// of the series f(n)= (1) + (2*3)
// + (4*5*6) ... n using recursion
#include <stdio.h>

// Recursive function for
// finding sum of series
// calculated - number of terms till
//                which sum of terms has
//              been calculated
// current - number of terms for which
//             sum has to becalculated
// N         - Number of terms in the
//             function to be calculated
int seriesSum(int calculated, int current,
                              int N)
{
    int i, cur = 1;

    // checking termination condition
    if (current == N + 1)
        return 0;

    // product of terms till current
    for (i = calculated; i < calculated +
                            current; i++)
        cur *= i;

    // recursive call for adding
    // terms next in the series
    return cur + seriesSum(i, current + 1, N);
}

// Driver Code
int main()
{
    // input number of terms in the series
    int N = 5;

    // invoking the function to
    // calculate the sum
    printf("%d\n", seriesSum(1, 1, N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the
// solution of the series
// f(n)= (1) + (2*3) + (4*5*6)
// ... n using recursion

class GFG
{

    /**
    * Recursive method for finding
    * sum of series
    *
    * @param calculated number of terms
    * till which sum of terms has been
    * calculated @param current number of
    * terms for which sum has to be calculated.
    * @param N Number of terms in the function
    * to be calculated @return sum
    */

    static int seriesSum(int calculated,
                         int current,
                         int N)
    {
        int i, cur = 1;

        // checking termination condition
        if (current == N + 1)
            return 0;

        // product of terms till current
        for (i = calculated; i < calculated +
                                current; i++)
            cur *= i;

        // recursive call for adding
        // terms next in the series
        return cur + seriesSum(i, current + 1, N);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // input number of
        // terms in the series
        int N = 5;

        // invoking the method
        // to calculate the sum
        System.out.println(seriesSum(1, 1, N));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to print the solution
# of the series f(n)= (1) + (2*3) + (4*5*6)
# ... n using recursion

# Recursive function for finding sum of series
# calculated - number of terms till
#               which sum of terms
#               has been calculated
# current - number of terms for
#            which sum has to be
#            calculated
# N     - Number of terms in the
#       function to be calculated
def seriesSum(calculated, current, N):

    i = calculated;
    cur = 1;

    # checking termination condition
    if (current == N + 1):
        return 0;

    # product of terms till current
    while (i < calculated + current):
        cur *= i;
        i += 1;

    # recursive call for adding
    # terms next in the series
    return cur + seriesSum(i, current + 1, N);

# Driver code

# input number of terms in the series
N = 5;

# invoking the function
# to calculate the sum
print(seriesSum(1, 1, N));

# This code is contributed by mits
```

## C#

```
// C# Program to print the
// solution of the series
// f(n)= (1) + (2*3) + (4*5*6)
// ... n using recursion
using System;

class GFG
{

    // Recursive function for
    // finding sum of series
    // calculated - number of terms till 
    //                which sum of terms
    //              has been calculated
    // current    - number of terms for which
    //                sum has to be calculated
    // N         - Number of terms in the 
    //               function to be calculated
    static int seriesSum(int calculated,
                         int current,
                         int N)
    {

        int i, cur = 1;

        // checking termination condition
        if (current == N + 1)
            return 0;

        // product of terms till current
        for (i = calculated; i < calculated +
                                current; i++)
            cur *= i;

        // recursive call for adding terms
        // next in the series
        return cur + seriesSum(i, current + 1, N);
    }

    // Driver Code
    public static void Main()
    {

        // input number of terms
        // in the series
        int N = 5;

        // invoking the method to
        // calculate the sum
        Console.WriteLine(seriesSum(1, 1, N));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print the
// solution of the series
// f(n)= (1) + (2*3) + (4*5*6)
// ... n using recursion

// Recursive function for
// finding sum of series
// calculated - number of terms till
//                which sum of terms
//              has been calculated
// current -    number of terms for
//                which sum has to be
//              calculated
// N         - Number of terms in the
//             function to be calculated
function seriesSum($calculated, $current, $N)
{
    $i; $cur = 1;

    // checking termination condition
    if ($current == $N + 1)
        return 0;

    // product of terms till current
    for ($i = $calculated; $i < $calculated +
                              $current; $i++)
        $cur *= $i;

    // recursive call for adding
    // terms next in the series
    return $cur + seriesSum($i, $current + 1, $N);
}

// Driver code

// input number of
// terms in the series
$N = 5;

// invoking the function
// to calculate the sum
echo(seriesSum(1, 1, $N));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to print the
// solution of the series
// f(n)= (1) + (2*3) + (4*5*6)
// ... n using recursion

/**
    * Recursive method for finding
    * sum of series
    *
    * @param calculated number of terms
    * till which sum of terms has been
    * calculated @param current number of
    * terms for which sum has to be calculated.
    * @param N Number of terms in the function
    * to be calculated @return sum
    */

    function seriesSum(calculated,
                         current, N)
    {
        let i, cur = 1;

        // checking termination condition
        if (current == N + 1)
            return 0;

        // product of terms till current
        for (i = calculated; i < calculated +
                                current; i++)
            cur *= i;

        // recursive call for adding
        // terms next in the series
        return cur + seriesSum(i, current + 1, N);
    }

// Driver Code

        // input number of
        // terms in the series
        let N = 5;

        // invoking the method
        // to calculate the sum
        document.write(seriesSum(1, 1, N));

    // This code is contributed by target_2.
</script>
```

**输出:**

```
365527 
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息