# 处理溢出的整数的倒位数

> 原文:[https://www . geesforgeks . org/reverse-digits-integer-overflow-handled/](https://www.geeksforgeeks.org/reverse-digits-integer-overflow-handled/)

假设输入是 32 位整数，编写一个程序来反转整数。如果反转的整数溢出，打印-1 作为输出。
让我们来看一个[反转整数位数的简单方法](https://www.geeksforgeeks.org/write-a-c-program-to-reverse-digits-of-a-number)。

## C++

```
// A simple C program to reverse digits of
// an integer.
#include <stdio.h>

int reversDigits(int num)
{
    int rev_num = 0;
    while (num > 0)
    {
        rev_num = rev_num*10 + num%10;
        num = num/10;
    }
    return rev_num;
}

/* Driver program to test reversDigits */
int main()
{
    int num = 5896;
    printf("Reverse of no. is %d", reversDigits(num));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a number

class GFG
{
    /* Iterative function to reverse
    digits of num*/
    static int reversDigits(int num)
    {
        int rev_num = 0;
        while(num > 0)
        {
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }
        return rev_num;
    }

    // Driver code
    public static void main (String[] args)
    {
        int num = 4562;
        System.out.println("Reverse of no. is "
                           + reversDigits(num));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to reverse a number

n = 4562;
rev = 0

while(n > 0):
    a = n % 10
    rev = rev * 10 + a
    n = n / 10

print(rev)

# This code is contributed by Shariq Raza
```

## C#

```
// C# program to reverse a number
using System;

class GFG
{
    // Iterative function to
    // reverse digits of num
    static int reversDigits(int num)
    {
        int rev_num = 0;
        while(num > 0)
        {
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }
        return rev_num;
    }

    // Driver code
    public static void Main()
    {
        int num = 4562;
        Console.Write("Reverse of no. is "
                        + reversDigits(num));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative function to
// reverse digits of num
function reversDigits($num)
{
    $rev_num = 0;
    while($num > 1)
    {
        $rev_num = $rev_num * 10 +
                        $num % 10;
        $num = (int)$num / 10;
    }
    return $rev_num;
}

// Driver Code
$num = 4562;
echo "Reverse of no. is ",
       reversDigits($num);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to reverse digits of
// an integer.

function reversDigits(num)
{
    let rev_num = 0;
    while (num > 0)
    {
        rev_num = rev_num*10 + num%10;
        num = Math.floor(num/10);
    }
    return rev_num;
}

/* Driver program to test reversDigits */

    let num = 5896;
    document.write("Reverse of no. is "+ reversDigits(num));

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
Reverse of no. is 6985
```

但是，如果数量很大，以至于反向溢出，则输出是一些垃圾值。如果我们运行上面的代码，输入任意大的数字，比如 **1000000045** ，那么输出就是一些垃圾值，比如 **1105032705** 或者任何其他垃圾值。输出见[本](https://ide.geeksforgeeks.org/moL71L)。
*如何处理溢出？*
思路是把之前的和的值可以存储在一个变量中，每次都可以检查一下，看看反向是否溢出。
以下是应对这种情况的实施方案。

## C++

```
// C++ program to reverse digits
// of a number
#include <bits/stdc++.h>

using namespace std;

/* Iterative function to reverse
digits of num*/
int reversDigits(int num)
{
    // Handling negative numbers
    bool negativeFlag = false;
    if (num < 0)
    {
        negativeFlag = true;
        num = -num ;
    }

    int prev_rev_num = 0, rev_num = 0;
    while (num != 0)
    {
        int curr_digit = num % 10;

        rev_num = (rev_num * 10) + curr_digit;

        // checking if the reverse overflowed or not.
        // The values of (rev_num - curr_digit)/10 and
        // prev_rev_num must be same if there was no
        // problem.
        if ((rev_num - curr_digit) /
               10 != prev_rev_num)
        {
            cout << "WARNING OVERFLOWED!!!"
                 << endl;
            return 0;
        }

        prev_rev_num = rev_num;
        num = num / 10;
    }

    return (negativeFlag == true) ?
                         -rev_num : rev_num;
}

// Driver Code
int main()
{
    int num = 12345;
    cout << "Reverse of no. is "
         << reversDigits(num) << endl;

    num = 1000000045;
    cout << "Reverse of no. is "
         << reversDigits(num) << endl;

    return 0;
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## C

```
// C program to reverse digits of a number
#include <stdio.h>

/* Iterative function to reverse digits of num*/
int reversDigits(int num)
{
    // Handling negative numbers
    bool negativeFlag = false;
    if (num < 0)
    {
        negativeFlag = true;
        num = -num ;
    }

    int prev_rev_num = 0, rev_num = 0;
    while (num != 0)
    {
        int curr_digit = num%10;

        rev_num = (rev_num*10) + curr_digit;

        // checking if the reverse overflowed or not.
        // The values of (rev_num - curr_digit)/10 and
        // prev_rev_num must be same if there was no
        // problem.
        if ((rev_num - curr_digit)/10 != prev_rev_num)
        {
            printf("WARNING OVERFLOWED!!!\n");
            return 0;
        }

        prev_rev_num = rev_num;
        num = num/10;
    }

    return (negativeFlag == true)? -rev_num : rev_num;
}

/* Driver program to test reverse Digits */
int main()
{
    int num = 12345;
    printf("Reverse of no. is %d\n", reversDigits(num));

    num = 1000000045;
    printf("Reverse of no. is %d\n", reversDigits(num));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse digits of a number

class ReverseDigits
{
    /* Iterative function to reverse digits of num*/
    static int reversDigits(int num)
    {
        // Handling negative numbers
        boolean negativeFlag = false;
        if (num < 0)
        {
            negativeFlag = true;
            num = -num ;
        }

        int prev_rev_num = 0, rev_num = 0;
        while (num != 0)
        {
            int curr_digit = num%10;

            rev_num = (rev_num*10) + curr_digit;

            // checking if the reverse overflowed or not.
            // The values of (rev_num - curr_digit)/10 and
            // prev_rev_num must be same if there was no
            // problem.
            if ((rev_num - curr_digit)/10 != prev_rev_num)
            {
                System.out.println("WARNING OVERFLOWED!!!");
                return 0;
            }

            prev_rev_num = rev_num;
            num = num/10;
        }

        return (negativeFlag == true)? -rev_num : rev_num;
    }

    public static void main (String[] args)
    {
        int num = 12345;
        System.out.println("Reverse of no. is " + reversDigits(num));

        num = 1000000045;
        System.out.println("Reverse of no. is " + reversDigits(num));
    }
}
```

## 蟒蛇 3

```
# Python program to reverse digits
# of a number

""" Iterative function to reverse
digits of num"""
def reversDigits(num):

    # Handling negative numbers
    negativeFlag = False
    if (num < 0):

        negativeFlag = True
        num = -num

    prev_rev_num = 0
    rev_num = 0
    while (num != 0):

        curr_digit = num % 10

        rev_num = (rev_num * 10) + curr_digit

        # checking if the reverse overflowed or not.
        # The values of (rev_num - curr_digit)/10 and
        # prev_rev_num must be same if there was no
        # problem.
        if (rev_num >= 2147483647 or
            rev_num <= -2147483648):
            rev_num = 0
        if ((rev_num - curr_digit) // 10 != prev_rev_num):

            print("WARNING OVERFLOWED!!!")
            return 0

        prev_rev_num = rev_num
        num = num //10

    return -rev_num if (negativeFlag == True) else rev_num

# Driver code
if __name__ =="__main__":
    num = 12345
    print("Reverse of no. is ",reversDigits(num))

    num = 1000000045
    print("Reverse of no. is ",reversDigits(num))

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to reverse digits
// of a number
using System;

class GFG
{

/* Iterative function to reverse
   digits of num*/
static int reversDigits(int num)
{
    // Handling negative numbers
    bool negativeFlag = false;
    if (num < 0)
    {
        negativeFlag = true;
        num = -num ;
    }

    int prev_rev_num = 0, rev_num = 0;
    while (num != 0)
    {
        int curr_digit = num % 10;

        rev_num = (rev_num * 10) +
                   curr_digit;

        // checking if the reverse overflowed
        // or not. The values of (rev_num -
        // curr_digit)/10 and prev_rev_num must
        // be same if there was no problem.
        if ((rev_num - curr_digit) / 10 != prev_rev_num)
        {
            Console.WriteLine("WARNING OVERFLOWED!!!");
            return 0;
        }

        prev_rev_num = rev_num;
        num = num / 10;
    }

    return (negativeFlag == true) ?
                         -rev_num : rev_num;
}

// Driver Code
static public void Main ()
{
    int num = 12345;
    Console.WriteLine("Reverse of no. is " +
                         reversDigits(num));

    num = 1000000045;
    Console.WriteLine("Reverse of no. is " +
                         reversDigits(num));
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>
// JavaScript program to reverse digits
// of a number

/* Iterative function to reverse
digits of num*/
function reversDigits(num)
{
    // Handling negative numbers
    let negativeFlag = false;
    if (num < 0)
    {
        negativeFlag = true;
        num = -num ;
    }

    let prev_rev_num = 0, rev_num = 0;
    while (num != 0)
    {
        let curr_digit = num % 10;

        rev_num = (rev_num * 10) + curr_digit;

        // checking if the reverse overflowed or not.
        // The values of (rev_num - curr_digit)/10 and
        // prev_rev_num must be same if there was no
        // problem.
        if (rev_num >= 2147483647 ||
            rev_num <= -2147483648)
            rev_num = 0;
        if (Math.floor((rev_num - curr_digit) / 10) != prev_rev_num)
        {
            document.write("WARNING OVERFLOWED!!!"
                + "<br>");
            return 0;
        }

        prev_rev_num = rev_num;
        num = Math.floor(num / 10);
    }

    return (negativeFlag == true) ?
                        -rev_num : rev_num;
}

// Driver Code
    let num = 12345;
    document.write("Reverse of no. is "
        + reversDigits(num) + "<br>");

    num = 1000000045;
    document.write("Reverse of no. is "
        + reversDigits(num) + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output**

```
Reverse of no. is 54321
WARNING OVERFLOWED!!!
Reverse of no. is 0

```