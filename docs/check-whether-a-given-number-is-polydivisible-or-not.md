# 检查给定的数字是否可见

> 原文:[https://www . geeksforgeeks . org/check-给定的数字是否是多可见的/](https://www.geeksforgeeks.org/check-whether-a-given-number-is-polydivisible-or-not/)

给定一个整数 n，找出 n 是否是一个聚二可见的。在数学中，如果一个数遵循一些独特的性质，它就被称为**聚二可见**。该数字不应有任何前导零。输入数字的前 I 位组成的数字应能被 I 整除，其中![i > 1 ~and ~i <= number ~of ~digits ~in ~the ~input ~number ](img/67a764c21841f1e3f75f14233e0e569c.png "Rendered by QuickLaTeX.com")。如果任何一个数遵循这些性质，那么它被称为**聚二可见数**。
**例:**

```
Input: 345654
Output: 345654 is Polydivisible number.
Explanation: 
The first digit of the number is non-zero. 
The number formed by the first 2 digits(34) 
is divisible by 2\. The number formed by the
first 3 digits(345) is divisible by 3\. 
The number formed by the first 4 digits(3456)
is divisible by 4\. The number formed by the
first 5 digits(34565) is divisible by 5\. 
The number formed by the first 6 digits(345654)
is divisible by 6\.     

Input: 130
Output: 130 is Not Polydivisible number.

Input: 129
Output: 129 is Polydivisible number.    
```

**做法:**思路很简单。

> 1.  Extract all the numbers of the array and store them in an array.
> 2.  Take the first two digits to form a number, and check whether it can be evenly divided by 2.
> 3.  Select the second number, attach it to the existing number, and check whether the number is divisible by I.
> 4.  If all the above conditions are met until all the numbers are used up, the given number is visible.

下面是上述方法的实现。

## C++

```
// CPP program to check whether
// a number is polydivisible or not
#include <bits/stdc++.h>
using namespace std;

// function to check polydivisible
// number
void check_polydivisible(int n)
{
    int N = n;
    vector<int> digit;

    // digit extraction of input number
    while (n > 0) {

        // store the digits in an array
        digit.push_back(n % 10);
        n /= 10;
    }
    reverse(digit.begin(), digit.end());

    bool flag = true;
    n = digit[0];
    for (int i = 1; i < digit.size(); i++) {

        // n contains first i digits
        n = n * 10 + digit[i];

        // n should be divisible by i
        if (n % (i + 1) != 0) {
            flag = false;
            break;
        }
    }
    if (flag)
        cout << N << " is Polydivisible number.";
    else
        cout << N << " is Not Polydivisible number.";
}

int main()
{
    int n = 345654;
    check_polydivisible(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// a number is polydivisible or not
import java.util.*;
import java.io.*;

class GFG {

    // function to check polydivisible
    // number
    static void check_polydivisible(int n)
    {
        int N = n;
        Vector<Integer> digit = new Vector<Integer>();

        // digit extraction of input number
        while (n > 0) {

            // store the digits in an array
            digit.add(new Integer(n % 10));
            n /= 10;
        }
        Collections.reverse(digit);

        boolean flag = true;
        n = digit.get(0);
        for (int i = 1; i < digit.size(); i++) {

            // n contains first i digits
            n = n * 10 + digit.get(i);

            // n should be divisible by i
            if (n % (i + 1) != 0) {
                flag = false;
                break;
            }
        }
        if (flag)
            System.out.println(N + " is Polydivisible number.");
        else
            System.out.println(N + " is Not Polydivisible number.");
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 345654;
        check_polydivisible(n);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check whether
# a number is polydivisible or not

# function to check polydivisible
# number
def check_polydivisible(n):
    N = n
    digit = []

    # digit extraction of input number
    while (n > 0):

        # store the digits in an array
        digit.append(n % 10)
        n /= 10

    digit.reverse()

    flag = True
    n = digit[0]
    for i in range(1, len(digit), 1):

        # n contains first i digits
        n = n * 10 + digit[i]

        # n should be divisible by i
        if (n % (i + 1) != 0):
            flag = False
            break

    if (flag):
        print(N, "is Polydivisible number.");
    else:
        print(N, "is Not Polydivisible number.")

# Driver Code
if __name__ == '__main__':
    n = 345654
    check_polydivisible(n)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to check whether
// a number is polydivisible or not
using System;
using System.Collections.Generic;

class GFG
{

    // function to check polydivisible
    // number
    static void check_polydivisible(int n)
    {
        int N = n;
        List<int> digit = new List<int>();

        // digit extraction of input number
        while (n > 0)
        {

            // store the digits in an array
            digit.Add((int)n % 10);
            n /= 10;
        }
        digit.Reverse();

        bool flag = true;
        n = digit[0];
        for (int i = 1; i < digit.Count; i++)
        {

            // n contains first i digits
            n = n * 10 + digit[i];

            // n should be divisible by i
            if (n % (i + 1) != 0)
            {
                flag = false;
                break;
            }
        }
        if (flag)
            Console.WriteLine(N +
                    " is Polydivisible number.");
        else
            Console.WriteLine(N +
                    " is Not Polydivisible number.");
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 345654;
        check_polydivisible(n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to check whether
    // a number is polydivisible or not

    // function to check polydivisible
    // number
    function check_polydivisible(n)
    {
        let N = n;
        let digit = [];

        // digit extraction of input number
        while (n > 0)
        {

            // store the digits in an array
            digit.push(n % 10);
            n = parseInt(n / 10, 10);
        }
        digit.reverse();

        let flag = true;
        n = digit[0];
        for (let i = 1; i < digit.length; i++)
        {

            // n contains first i digits
            n = n * 10 + digit[i];

            // n should be divisible by i
            if (n % (i + 1) != 0)
            {
                flag = false;
                break;
            }
        }
        if (flag)
            document.write(N + " is Polydivisible number." + "</br>");
        else
            document.write(N + " is Not Polydivisible number.");
    }

    let n = 345654;
      check_polydivisible(n);

</script>
```

**Output:** 

```
345654 is Polydivisible number.
```