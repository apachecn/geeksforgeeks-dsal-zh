# 递归程序，打印所有小于 N 且仅由数字 1 或 3 组成的数字

> 原文:[https://www . geesforgeks . org/递归-程序-打印-所有数字-小于-n-仅由数字-1 或-3 组成/](https://www.geeksforgeeks.org/recursive-program-to-print-all-numbers-less-than-n-which-consist-of-digits-1-or-3-only/)

给定一个整数 **N** ，任务是打印所有数字 **≤ N** ，它们的数字只有 **1** 或 **3** 。
**举例:**

> **输入:** N = 10
> **输出:** 3 1
> **输入:** N = 20
> **输出:** 13 11 3 1

**进场:**

*   首先，检查数字是否大于 0。如果是，则继续，否则程序终止。
*   检查号码的每个位置是否有数字 1 或 3。
*   如果我们在数字的每个位置找到 1 或 3，那么就打印这个数字。现在，通过递归调用比当前数字小 1 的数字来检查下一个数字。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Recursive function to print the desired numbers
void printNumbers(int N)
{

    // Bool variable to track whether each digit of
    // the number fulfills the given condition
    bool flag = 1;

    // Creating a copy of the number
    int x = N;

    // Checking if the number has a positive value
    if (N > 0) {

        // Loop to iterate through digits
        // of the number until every digit
        // fulfills the given condition
        while (x > 0 && flag == 1) {

            // Get last digit
            int digit = x % 10;

            // Updating value of flag to be 0 if
            // the digit is neither 1 nor 3
            if (digit != 1 && digit != 3)
                flag = 0;

            // Eliminate last digit
            x = x / 10;
        }

        // If N consists of digits 1 or 3 only
        if (flag == 1)
            cout << N << " ";

        // Recursive call for the next number
        printNumbers(N - 1);
    }
}

// Driver code
int main()
{
    int N = 20;
    printNumbers(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    // Recursive function to print the desired numbers
    static void printNumbers(int N)
    {

        // flag variable to track whether each digit of
        // the number fulfills the given condition
        int flag = 1;

        // Creating a copy of the number
        int x = N;

        // Checking if the number has a positive value
        if (N > 0)
        {

            // Loop to iterate through digits
            // of the number until every digit
            // fulfills the given condition
            while (x > 0 && flag == 1)
            {
                // Get last digit
                int digit = x % 10;

                // Updating value of flag to be 0 if
                // the digit is neither 1 nor 3
                if (digit != 1 && digit != 3)
                {
                    flag = 0;
                }

                // Eliminate last digit
                x = x / 10;
            }

            // If N consists of digits 1 or 3 only
            if (flag == 1) {
                System.out.print(N + " ");
            }

            // Recursive call for the next number
            printNumbers(N - 1);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 20;
        printNumbers(N);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Recursive function to print the
# desired numbers
def printNumbers(N):

    # Bool variable to track whether each digit
    # of the number fulfills the given condition
    flag = 1

    # Creating a copy of the number
    x = N

    # Checking if the number has a
    # positive value
    if (N > 0):

        # Loop to iterate through digits
        # of the number until every digit
        # fulfills the given condition
        while (x > 0 and flag == 1):

            # Get last digit
            digit = x % 10

            # Updating value of flag to be 0 if
            # the digit is neither 1 nor 3
            if (digit != 1 and digit != 3):
                flag = 0

            # Eliminate last digit
            x = x // 10

        # If N consists of digits 1 or 3 only
        if (flag == 1):
            print(N, end = " ")

        # Recursive call for the next number
        printNumbers(N - 1)

# Driver code
if __name__ == '__main__':
    N = 20
    printNumbers(N)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Recursive function to print the desired numbers
    static void printNumbers(int N)
    {
        // flag variable to track whether each digit of
        // the number fulfills the given condition
        int flag = 1;

        // Creating a copy of the number
        int x = N;

        // Checking if the number has a positive value
        if (N > 0)
        {
            // Loop to iterate through digits
            // of the number until every digit
            // fulfills the given condition
            while (x > 0 && flag == 1)
            {
                // Get last digit
                int digit = x % 10;

                // Updating value of flag to be 0 if
                // the digit is neither 1 nor 3
                if (digit != 1 && digit != 3)
                    flag = 0;

                // Eliminate last digit
                x = x / 10;
            }

            // If N consists of digits 1 or 3 only
            if (flag == 1)
                Console.Write(N + " ");

            // Recursive call for the next number
            printNumbers(N - 1);
        }
    }

    // Driver code
    public static void Main()
    {
            int N = 20;
            printNumbers(N);
    }
}

 // This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Recursive function to print the
// desired numbers
function printNumbers($N)
{

    // Bool variable to track whether each
    // digit of the number fulfills the
    // given condition
    $flag = 1;

    // Creating a copy of the number
    $x = $N;

    // Checking if the number has a
    // positive value
    if ($N > 0)
    {

        // Loop to iterate through digits
        // of the number until every digit
        // fulfills the given condition
        while ((int)$x > 0 && $flag == 1)
        {

            // Get last digit
            $digit = $x % 10;

            // Updating value of flag to be 0
            // if the digit is neither 1 nor 3
            if ($digit != 1 && $digit != 3)
                $flag = 0;

            // Eliminate last digit
            $x = $x / 10;
        }

        // If N consists of digits 1 or 3 only
        if ($flag == 1)
        {
            echo $N ;
            echo " ";
        }

        // Recursive call for the next number
        printNumbers($N - 1);
    }
}

// Driver code
$N = 20;
printNumbers($N);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Recursive function to print the desired numbers
    function printNumbers(N)
    {
        // flag variable to track whether each digit of
        // the number fulfills the given condition
        let flag = 1;

        // Creating a copy of the number
        let x = N;

        // Checking if the number has a positive value
        if (N > 0)
        {
            // Loop to iterate through digits
            // of the number until every digit
            // fulfills the given condition
            while (x > 0 && flag == 1)
            {
                // Get last digit
                let digit = x % 10;

                // Updating value of flag to be 0 if
                // the digit is neither 1 nor 3
                if (digit != 1 && digit != 3)
                    flag = 0;

                // Eliminate last digit
                x = parseInt(x / 10, 10);
            }

            // If N consists of digits 1 or 3 only
            if (flag == 1)
                document.write(N + " ");

            // Recursive call for the next number
            printNumbers(N - 1);
        }
    }

    let N = 20;
      printNumbers(N);

</script>
```

**Output:** 

```
13 11 3 1
```

请注意，这篇文章的想法是解释递归解决方案，有一个更好的方法来解决这个问题。我们可以使用队列来有效地解决这个问题。有关有效方法的详细信息，请参考[小于 N 的二进制数字的计数](https://www.geeksforgeeks.org/count-binary-digit-numbers-smaller-n/)。