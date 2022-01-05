# 寻找前 N 个 Iccanobif 号码的程序

> 原文:[https://www . geesforgeks . org/program-to-find-first-n-iccanobif-numbers/](https://www.geeksforgeeks.org/program-to-find-first-n-iccanobif-numbers/)

给定一个数字 N，任务是首先找到 N 个 **Iccanobif 数字**。
Iccanobif 数与斐波那契数相似。**第 K 个 Iccanobif 号码**可以通过前两个号码的数字反转后相加得到。
前几个 Iccanobif 编号为:

> 0, 1, 1, 2, 3, 5, 8, 13, 39, 124, 514, 836, …..

**示例** :

```
Input : N = 5
Output : 0 1 1 2 3

Input : N = 9
Output : 0 1 1 2 3 5 8 13 39
Explanation: Upto 8th term, adding previous two 
terms is required, as there is an only single digit. 
For 9th term, adding 31(reversing 8th term) 
and 8 will give 39.
```

**方法:**思路是取前两个 Iccanobif 数为**第一个= 0****第二个= 1** 。现在，使用演示指针迭代 N-2 次，每次使用在[中讨论的方法找到前面两个数字的反转:反转一个数字的数字](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)。求两个反转数之和，相应更新变量*第一个*和*第二个*。
以下是上述方法的实施:

## C++

```
// C++ program to find first
// N Icanobif numbers

#include <bits/stdc++.h>

using namespace std;

// Iterative function to
// reverse digits of num
int reversDigits(int num)
{
    int rev_num = 0;

    while (num > 0) {
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }

    return rev_num;
}

// Function to print first
// N Icanobif Numbers
void icanobifNumbers(int N)
{
    // Initialize first, second numbers
    int first = 0, second = 1;

    if (N == 1)
        cout << first;
    else if (N == 2)
        cout << first << " " << second;
    else {
        // Print first two numbers
        cout << first << " " << second << " ";

        for (int i = 3; i <= N; i++) {

            // Reversing digit of previous
            // two terms and adding them
            int x = reversDigits(first);
            int y = reversDigits(second);

            cout << x + y << " ";

            int temp = second;
            second = x + y;
            first = temp;
        }
    }
}

// Driver Code
int main()
{
    int N = 12;

    icanobifNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first
// N Icanobif numbers

public class GFG{

    // Iterative function to
    // reverse digits of num
    static int reversDigits(int num)
    {
        int rev_num = 0;

        while (num > 0) {
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }

        return rev_num;
    }

    // Function to print first
    // N Icanobif Numbers
    static void icanobifNumbers(int N)
    {
        // Initialize first, second numbers
        int first = 0, second = 1;

        if (N == 1)
            System.out.print(first);
        else if (N == 2)
             System.out.print(first + " " + second);
        else {
            // Print first two numbers
            System.out.print(first + " " + second + " ");

            for (int i = 3; i <= N; i++) {

                // Reversing digit of previous
                // two terms and adding them
                int x = reversDigits(first);
                int y = reversDigits(second);

                 System.out.print(x + y + " ");

                int temp = second;
                second = x + y;
                first = temp;
            }
        }
    }

    // Driver Code
    public static void main(String []args){
        int N = 12;

        icanobifNumbers(N);
     }
     // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to find first
# N Icanobif numbers

# Iterative function to
# reverse digits of num
def reversedigit(num):
    rev_num = 0
    while num > 0:
        rev_num = rev_num * 10 + num % 10
        num = num // 10
    return rev_num

# Function to print first
# N Icanobif Numbers
def icanobifNumbers(N):

    # Initialize first, second numbers
    first = 0
    second = 1
    if N == 1:
        print(first)
    elif N == 2:
        print(first, second)
    else:

        # Print first two numbers
        print(first, second, end = " ")
        for i in range(3, N + 1):

            # Reversing digit of previous
            # two terms and adding them
            x = reversedigit(first)
            y = reversedigit(second)
            print(x + y, end = " ")
            temp = second
            second = x + y
            first = temp

# Driver code
N = 12
icanobifNumbers(N)

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find first
// N Icanobif numbers

using System;
public class GFG{

    // Iterative function to
    // reverse digits of num
    static int reversDigits(int num)
    {
        int rev_num = 0;

        while (num > 0) {
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }

        return rev_num;
    }

    // Function to print first
    // N Icanobif Numbers
    static void icanobifNumbers(int N)
    {
        // Initialize first, second numbers
        int first = 0, second = 1;

        if (N == 1)
            Console.Write(first);
        else if (N == 2)
             Console.Write(first + " " + second);
        else {
            // Print first two numbers
            Console.Write(first + " " + second + " ");

            for (int i = 3; i <= N; i++) {

                // Reversing digit of previous
                // two terms and adding them
                int x = reversDigits(first);
                int y = reversDigits(second);

                 Console.Write(x + y + " ");

                int temp = second;
                second = x + y;
                first = temp;
            }
        }
    }

    // Driver Code
    public static void Main(){
        int N = 12;

        icanobifNumbers(N);
     }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find first N
// Icanobif numbers

// Iterative function to reverse
// digits of num
function reversDigits($num)
{
    $rev_num = 0;

    while ($num > 0)
    {
        $rev_num = ($rev_num * 10) +
                       ($num % 10);
        $num = (int)( $num / 10);
    }

    return $rev_num;
}

// Function to print first
// N Icanobif Numbers
function icanobifNumbers($N)
{
    // Initialize first, second numbers
    $first = 0;
    $second = 1;

    if ($N == 1)
    echo $first;
    else if ($N == 2)
        echo $first , " ", $second;
    else
    {
        // Print first two numbers
        echo $first, " " , $second, " ";

        for ($i = 3; $i <= $N; $i++)
        {

            // Reversing digit of previous
            // two terms and adding them
            $x = reversDigits($first);
            $y = reversDigits($second);

            echo ($x + $y), " ";

            $temp = $second;
            $second = $x + $y;
            $first = $temp;
        }
    }
}

// Driver Code
$N = 12;
icanobifNumbers($N);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find first
    // N Icanobif numbers

    // Iterative function to
    // reverse digits of num
    function reversDigits(num)
    {
        let rev_num = 0;

        while (num > 0) {
            rev_num = rev_num * 10 + num % 10;
            num = parseInt(num / 10, 10);
        }

        return rev_num;
    }

    // Function to print first
    // N Icanobif Numbers
    function icanobifNumbers(N)
    {
        // Initialize first, second numbers
        let first = 0, second = 1;

        if (N == 1)
            document.write(first);
        else if (N == 2)
             document.write(first + " " + second);
        else {
            // Print first two numbers
            document.write(first + " " + second + " ");

            for (let i = 3; i <= N; i++) {

                // Reversing digit of previous
                // two terms and adding them
                let x = reversDigits(first);
                let y = reversDigits(second);

                  document.write(x + y + " ");

                let temp = second;
                second = x + y;
                first = temp;
            }
        }
    }

    let N = 12;

      icanobifNumbers(N);

</script>
```

**Output:** 

```
0 1 1 2 3 5 8 13 39 124 514 836
```

**注**:对于较大的 N 值，使用数字作为字符串。