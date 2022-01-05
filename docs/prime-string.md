# 质数串

> 原文:[https://www.geeksforgeeks.org/prime-string/](https://www.geeksforgeeks.org/prime-string/)

给定一个字符串 **str** ，任务是检查所有字符的 ASCII 值之和是否为[质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。

**例:**

```
Input  : geeksforgeeks
Output : Yes
Input  : GeeksForGeeks
Output : No
```

**算法**

1.  Calculate string length
2.  Calculate the sum of ASCII values of all characters
3.  Now we can check n <sup>1/2</sup> because the larger factor of n must be a multiple of the smaller factor. (For details, see [Check whether the number is prime](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/) )
4.  If the sum is prime, print "Yes", otherwise print "No"

现将上述方法的实现给出如下:

## c++

```
// C++ program to find if string is a
// Prime or not.
#include <bits/stdc++.h>
using namespace std;

// Function that checks if sum
// is prime or not
bool isPrimeString(string str)
{
    int len = str.length(), n = 0;
    for (int i = 0; i < len; i++)
        n += (int)str[i];

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Driver code
int main()
{
    string str = "geekRam";
    if (isPrimeString(str))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

## Java

```
// Java program to find if
// string is a Prime or not.
import java.io.*;

class GFG {

    // Function that checks if
    // sum is prime or not
    static boolean isPrimeString(String str)
    {
        int len = str.length(), n = 0;
        for (int i = 0; i < len; i++)
            n += (int)str.charAt(i);

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "geekRam";

        if (isPrimeString(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Ajit.
```

## python 3

T2T19】c#T3T23】PHPT4

## Javascript

T5T31】

**输出:**

```
No
```