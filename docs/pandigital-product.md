# 泛数码产品

> 原文:[https://www.geeksforgeeks.org/pandigital-product/](https://www.geeksforgeeks.org/pandigital-product/)

一个[泛数字数字](https://www.geeksforgeeks.org/pandigital-number-given-base/)是所有数字 1 到 9 精确使用一次的数字。给我们一个数，我们需要找出是否有两个数的乘积是给定数，给定的三个数加起来是泛数。

**例:**

```
Input : 7254
Output : Yes
39 * 186 = 7254\. We can notice that
the three numbers 39, 186 and 7254
together have all digits from 1 to 9.

Input : 6952
Output : Yes

```

这个想法是考虑所有乘以给定数的对。对于每一对，创建一个包含三个数字的字符串(给定的数字和当前对)。我们对创建的字符串进行排序，并检查排序后的字符串是否等于“123456789”。

## c++

```
// C++ code to check the number
// is Pandigital Product or not
#include <bits/stdc++.h>
using namespace std;

// To check the string formed
// from multiplicand, multiplier
// and product is pandigital
bool isPandigital(string str)
{
    if (str.length() != 9)
        return false;

    char ch[str.length()];
    strcpy(ch, str.c_str());
    sort(ch, ch + str.length());
    string s = ch;

    if(s.compare("123456789") == 0)
        return true;
    else
        return true;
}

// calculate the multiplicand,
// multiplier, and product
// eligible for pandigital
bool PandigitalProduct_1_9(int n)
{
    for (int i = 1; i * i <= n; i++)
        if (n % i == 0 && isPandigital(to_string(n) +
                                       to_string(i) +
                                   to_string(n / i)))
            return true;
    return false;
}

// Driver Code
int main()
{
    int n = 6952;
    if (PandigitalProduct_1_9(n) == true)
        cout << "yes";
    else
        cout << "no";
    return 0;
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## Java

```
// Java code to check the number
// is Pandigital Product or not
import java.io.*;
import java.util.*;
class GFG {

    // calculate the multiplicand, multiplier, and product
    // eligible for pandigital
    public static boolean PandigitalProduct_1_9(int n)
    {
        for (int i = 1; i*i <= n; i++)
            if (n % i == 0 && isPandigital("" + n + i + n / i))
                return true;
        return false;
    }

    // To check the string formed from multiplicand
    // multiplier and product is pandigital
    public static boolean isPandigital(String str)
    {
        if (str.length() != 9)
            return false;
        char ch[] = str.toCharArray();
        Arrays.sort(ch);
        return new String(ch).equals("123456789");
    }

    // Driver function
    public static void main(String[] args)
    {
        int n = 6952;
        if (PandigitalProduct_1_9(n) == true)
            System.out.println("yes");
        else
            System.out.println("no");
    }
}
```

## python 3

T2T18】c#T20

```
// C# code to check the number
// is Pandigital Product or not.
using System;

class GFG {

    // calculate the multiplicand,
    // multiplier, and product
    // eligible for pandigital
    public static bool PandigitalProduct_1_9(int n)
    {
        for (int i = 1; i*i <= n; i++)
            if (n % i == 0 && isPandigital("" + n
                                      + i + n / i))
                return true;

        return false;
    }

    // To check the string formed from multiplicand
    // multiplier and product is pandigital
    public static bool isPandigital(String str)
    {
        if (str.Length != 9)
            return false;

        char []ch = str.ToCharArray();
        Array.Sort(ch);

        return new String(ch).Equals("123456789");
    }

    // Driver function
    public static void Main()
    {
        int n = 6952;

        if (PandigitalProduct_1_9(n) == true)
            Console.Write("yes");
        else
            Console.Write("no");
    }
}

// This code is contributed by nitin mittal.
```

T21

## PHP

T4T26】

**输出:**

```
yes

```