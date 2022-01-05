# 找出数字乘以给定数字 n 的最小数字

> 原文:[https://www . geesforgeks . org/find-最小数字-谁的数字-乘给定数字-n/](https://www.geeksforgeeks.org/find-smallest-number-whose-digits-multiply-given-number-n/)

给定一个数字“n”，求最小的数字“p”，这样，如果我们把“p”的所有数字相乘，就得到“n”。结果“p”应该至少有两位数。
**例:**

```
Input:  n = 36
Output: p = 49 
// Note that 4*9 = 36 and 49 is the smallest such number

Input:  n = 100
Output: p = 455
// Note that 4*5*5 = 100 and 455 is the smallest such number

Input: n = 1
Output:p = 11
// Note that 1*1 = 1

Input: n = 13
Output: Not Possible
```

对于给定的 n，下面是要考虑的两种情况。
**情况 1: n < 10** 当 n 小于 10 时，输出总是 n+10。例如，对于 n = 7，输出为 17。对于 n = 9，输出为 19。
**例 2: n > = 10** 求 n 的所有因子，均在 2 和 9 之间(含 2 和 9)。这个想法是从 9 开始搜索，这样结果中的位数就最小化了。例如，9 比 33 更优选，8 比 24 更优选。
将所有找到的因子存储在一个数组中。该数组将包含非递增顺序的数字，因此最后以相反的顺序打印该数组。
以下是上述概念的实现。

## C++

```
#include<bits/stdc++.h>
using namespace std;

// Maximum number of digits in output
#define MAX 50

// prints the smallest number
// whose digits multiply to n
void findSmallest(int n)
{
    int i, j = 0;

    // To store digits of result
    // in reverse order
    int res[MAX];

    // Case 1: If number is smaller than 10
    if (n < 10)
    {
        cout << n + 10;
        return;
    }

    // Case 2: Start with 9 and
    // try every possible digit
    for (i = 9; i > 1; i--)
    {
        // If current digit divides n, then store all
        // occurrences of current digit in res
        while (n % i == 0)
        {
            n = n / i;
            res[j] = i;
            j++;
        }
    }

    // If n could not be broken
    // in form of digits (prime factors
    // of n are greater than 9)
    if (n > 10)
    {
        cout << "Not possible";
        return;
    }

    // Print the result array in reverse order
    for (i = j - 1; i >= 0; i--)
        cout << res[i];
}

// Driver Code
int main()
{
    findSmallest(7);
    cout << "\n";

    findSmallest(36);
    cout << "\n";

    findSmallest(13);
    cout << "\n";

    findSmallest(100);
    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
#include<stdio.h>

// Maximum number of digits in output
#define MAX 50

// prints the smallest number whose digits multiply to n
void findSmallest(int n)
{
    int i, j=0;
    int res[MAX]; // To sore digits of result in reverse order

    // Case 1: If number is smaller than 10
    if (n < 10)
    {
        printf("%d", n+10);
        return;
    }

    // Case 2: Start with 9 and try every possible digit
    for (i=9; i>1; i--)
    {
        // If current digit divides n, then store all
        // occurrences of current digit in res
        while (n%i == 0)
        {
            n = n/i;
            res[j] = i;
            j++;
        }
    }

    // If n could not be broken in form of digits (prime factors of n
    // are greater than 9)
    if (n > 10)
    {
        printf("Not possible");
        return;
    }

    // Print the result array in reverse order
    for (i=j-1; i>=0; i--)
        printf("%d", res[i]);
}

// Driver program to test above function
int main()
{
    findSmallest(7);
    printf("\n");

    findSmallest(36);
    printf("\n");

    findSmallest(13);
    printf("\n");

    findSmallest(100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number whose
// digits multiply to a given number n

import java.io.*;

class Smallest
{
    // Function to prints the smallest number whose
    // digits multiply to n
    static void findSmallest(int n)
    {
        int i, j=0;
        int MAX = 50;
        // To sore digits of result in reverse order
        int[] res = new int[MAX];

        // Case 1: If number is smaller than 10
        if (n < 10)
        {
            System.out.println(n+10);
            return;
        }

        // Case 2: Start with 9 and try every possible digit
        for (i=9; i>1; i--)
        {
            // If current digit divides n, then store all
            // occurrences of current digit in res
            while (n%i == 0)
            {
                n = n/i;
                res[j] = i;
                j++;
            }
        }

        // If n could not be broken in form of digits (prime factors of n
        // are greater than 9)
        if (n > 10)
        {
            System.out.println("Not possible");
            return;
        }

        // Print the result array in reverse order
        for (i=j-1; i>=0; i--)
            System.out.print(res[i]);
        System.out.println();
    }

    // Driver program
    public static void main (String[] args)
    {
        findSmallest(7);
        findSmallest(36);
        findSmallest(13);
        findSmallest(100);
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python code to find the smallest number
# whose digits multiply to give n

# function to print the smallest number whose
# digits multiply to n
def findSmallest(n):
    # Case 1 - If the number is smaller than 10
    if n < 10:
        print n+10
        return

    # Case 2 - Start with 9 and try every possible digit
    res = [] # to sort digits
    for i in range(9,1,-1):
        # If current digit divides n, then store all
        # occurrences of current digit in res
        while n % i == 0:
            n = n / i
            res.append(i)

    # If n could not be broken in the form of digits
    # prime factors of  n are greater than 9

    if n > 10:
        print "Not Possible"
        return

    # Print the number from result array in reverse order
    n = res[len(res)-1]
    for i in range(len(res)-2,-1,-1):
        n = 10 * n + res[i]
    print n

# Driver Code
findSmallest(7)

findSmallest(36)

findSmallest(13)

findSmallest(100)

# This code is contributed by Harshit Agrawal
```

## C#

```
// C# program to find the smallest number whose
// digits multiply to a given number n
using System;

class GFG {

    // Function to prints the smallest number
    // whose digits multiply to n
    static void findSmallest(int n)
    {

        int i, j=0;
        int MAX = 50;

        // To sore digits of result in
        // reverse order
        int []res = new int[MAX];

        // Case 1: If number is smaller than 10
        if (n < 10)
        {
            Console.WriteLine(n + 10);
            return;
        }

        // Case 2: Start with 9 and try every
        // possible digit
        for (i = 9; i > 1; i--)
        {

            // If current digit divides n, then
            // store all occurrences of current
            // digit in res
            while (n % i == 0)
            {
                n = n / i;
                res[j] = i;
                j++;
            }
        }

        // If n could not be broken in form of
        // digits (prime factors of n
        // are greater than 9)
        if (n > 10)
        {
            Console.WriteLine("Not possible");
            return;
        }

        // Print the result array in reverse order
        for (i = j-1; i >= 0; i--)
            Console.Write(res[i]);

        Console.WriteLine();
    }

    // Driver program
    public static void Main ()
    {
        findSmallest(7);
        findSmallest(36);
        findSmallest(13);
        findSmallest(100);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// smallest number whose
// digits multiply to a
// given number n prints the
// smallest number whose digits
// multiply to n

function findSmallest($n)
{

    // To sore digits of
    // result in reverse order
    $i;
    $j = 0;
    $res;

    // Case 1: If number is
    // smaller than 10
    if ($n < 10)
    {
        echo $n + 10;
        return;
    }

    // Case 2: Start with 9 and
    // try every possible digit
    for ($i = 9; $i > 1; $i--)
    {

        // If current digit divides
        // n, then store all
        // occurrences of current
        // digit in res
        while ($n % $i == 0)
        {
            $n = $n / $i;
            $res[$j] = $i;
            $j++;
        }
    }

    // If n could not be broken
    // in form of digits
    // (prime factors of n
    // are greater than 9)
    if ($n > 10)
    {
        echo "Not possible";
        return;
    }

    // Print the result
    // array in reverse order
    for ($i = $j - 1; $i >= 0; $i--)
        echo $res[$i];
}

    // Driver Code
    findSmallest(7);
    echo "\n";

    findSmallest(36);

    echo "\n";

    findSmallest(13);
    echo "\n";

    findSmallest(100);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the smallest number whose 
// digits multiply to a given number n 

// Maximum number of digits in output 

// prints the smallest number
// whose digits multiply to n
function findSmallest(n)
{
    let i, j = 0;

    // To store digits of result
    // in reverse order
    let res = new Array(50);

    // Case 1: If number is smaller than 10
    if (n < 10)
    {
        document.write(n + 10);
        return;
    }

    // Case 2: Start with 9 and
    // try every possible digit
    for (i = 9; i > 1; i--)
    {
        // If current digit divides n, then store all
        // occurrences of current digit in res
        while (n % i == 0)
        {
            n = Math.floor(n / i);
            res[j] = i;
            j++;
        }
    }

    // If n could not be broken
    // in form of digits (prime factors
    // of n are greater than 9)
    if (n > 10)
    {
        document.write("Not possible");
        return;
    }

    // Print the result array in reverse order
    for (i = j - 1; i >= 0; i--)
        document.write(res[i]);
}

// Driver Code

    findSmallest(7);
    document.write("<br>");

    findSmallest(36);
    document.write("<br>");

    findSmallest(13);
    document.write("<br>");

    findSmallest(100);

// This code is contributed by Mayank Tyagi

</script>
```

输出:

```
17
49
Not possible
455 
```

时间复杂度:O(log <sub>2</sub> n * 10)

辅助空间:0(最大)

本文由 **Ashish Bansal** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息