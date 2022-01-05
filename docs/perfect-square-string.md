# 完美方形弦

> 原文:[https://www.geeksforgeeks.org/perfect-square-string/](https://www.geeksforgeeks.org/perfect-square-string/)

给定一个字符串**字符串**，任务是检查所有字符的 ASCII 值之和是否是一个完美的正方形。

**例:**

```
Input : ddddddddddddddddddddddddd
Output : Yes

Input : GeeksForGeeks
Output : No
```

**算法**

*   Calculate string length
*   Calculate the sum of ASCII values of all characters
*   Take the square root of the sum of numbers and store it in the variable SquareRoot
*   Take the square root of the floor value and subtract it from the square root
*   If the difference between the square root and the floor value of the square root is 0, print "Yes" or "No"

下面是上述方法的实现:

## c++

```
// C++ program to find if string is a
// perfect square or not.
#include <bits/stdc++.h>
using namespace std;

bool isPerfectSquareString(string str)
{
    int sum = 0;

    // calculating the length of
    // the string
    int len = str.length();

    // calculating the ASCII value
    // of the string
    for (int i = 0; i < len; i++)
        sum += (int)str[i];

    // Find floating point value of
    // square root of x.
    long double squareRoot = sqrt(sum);

    // If square root is an integer
    return ((squareRoot -
             floor(squareRoot)) == 0);
}

// Driver code
int main()
{
    string str = "d";

    if (isPerfectSquareString(str))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java

```
// Java program to find if string
// is a perfect square or not.
import java.io.*;

class GFG {

    static boolean isPerfectSquareString(String str)
    {
        int sum = 0;

        // calculating the length
        // of the string
        int len = str.length();

        // calculating the ASCII
        // value of the string
        for (int i = 0; i < len; i++)
            sum += (int)str.charAt(i);

        // Find floating point value
        // of square root of x.
        long squareRoot = (long)Math.sqrt(sum);

        // If square root is an integer
        return ((squareRoot -
                Math.floor(squareRoot)) == 0);
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "d";

        if (isPerfectSquareString(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Ajit.
```

## python 3

T2T20】c#T3T24】PHPT4

## Javascript

T5T32T34】输出