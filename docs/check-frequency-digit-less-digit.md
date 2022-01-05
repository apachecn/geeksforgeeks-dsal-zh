# 检查每个数字的频率是否小于数字

> 原文:[https://www . geesforgeks . org/check-frequency-digest-less-digest/](https://www.geeksforgeeks.org/check-frequency-digit-less-digit/)

给定一个整数 n，任务是检查数字的每个数字的频率是否小于或等于数字本身。
**例:**

```
Input : 51241
Output : False

Input : 1425243
Output : True
```

**天真方法:**从 0 开始，计算每一个数字的频率，直到 9，如果任何地方的频率大于数字值，则返回假，否则返回真。

## C++

```
// A C++ program to validate a number
#include<bits/stdc++.h>
using namespace std;

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
bool validate(long long int n)
{
    for (int i=0; i<10; i++)
    {
        long long int temp = n;
        int count = 0;
        while (temp)
        {
            // If current digit of temp is
            // same as i
            if (temp % 10 == i)
                count++;

            // if frequency is greater than
            // digit value, return false
            if (count > i)
                return false;

            temp /= 10;
        }
    }
    return true;
}

// driver program
int main()
{
    long long int n = 1552793;
    if (validate(n))
        cout << "True";
    else
        cout << "False";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate a number
import java .io.*;

public class GFG {

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
static boolean validate(long n)
{
    for (int i = 0; i < 10; i++)
    {
        long temp = n;
        int count = 0;
        while (temp > 0)
        {
            // If current digit of
            // temp is same as i
            if (temp % 10 == i)
                count++;

            // if frequency is greater than
            // digit value, return false
            if (count > i)
                return false;

            temp /= 10;
        }
    }
    return true;
}

    // Driver Code
    static public void main (String[] args)
    {
            long n = 1552793;
        if (validate(n))
            System.out.println("True");
        else
            System.out.println("False");
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to validate a number

# Function to validate number (Check if
# frequency of a digit is less than the
# digit itself or not)
def validate(n):

    for i in range(10):
        temp = n;
        count = 0;
        while (temp):

            # If current digit of temp is
            # same as i
            if (temp % 10 == i):
                count+=1;

            # if frequency is greater than
            # digit value, return false
            if (count > i):
                return -1;

            temp //= 10;

    return 1;

# Driver Code
n = 1552793;
geek = "True" if validate(n) else "False";
print(geek);

# This code is contributed by mits
```

## C#

```
// C# program to validate a number
using System;

public class GFG {

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
static bool validate(long n)
{
    for (int i = 0; i < 10; i++)
    {
        long temp = n;
        int count = 0;
        while (temp > 0)
        {
            // If current digit of
            // temp is same as i
            if (temp % 10 == i)
                count++;

            // if frequency is greater than
            // digit value, return false
            if (count > i)
                return false;

            temp /= 10;
        }
    }
    return true;
}

    // Driver Code
    static public void Main(String[] args)
    {
            long n = 1552793;
        if (validate(n))
            Console.WriteLine("True");
        else
            Console.WriteLine("False");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to validate a number

// Function to validate number
// (Check if frequency of a
// digit is less than the
// digit itself or not)
function validate($n)
{
    for ($i = 0; $i < 10; $i++)
    {
        $temp = $n;
        $count = 0;
        while ($temp)
        {

            // If current digit
            // of temp is same
            // as i
            if ($temp % 10 == $i)
                $count++;

            // if frequency is
            // greater than digit
            // value, return false
            if ($count > $i)
                return -1;

            $temp /= 10;
        }
    }
    return 1;
}

    // Driver Code
    $n = 1552793;
    $geek = validate($n) ?"True" :"False";
    echo($geek);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
function  validate(n)
{
    for (let i = 0; i < 10; i++)
    {
        let temp = n;
        let count = 0;
        while (temp > 0)
        {
            // If current digit of
            // temp is same as i
            if (temp % 10 == i)
                count++;

            // if frequency is greater than
            // digit value, return false
            if (count > i)
                return false;

            temp /= 10;
        }
    }
    return true;
}

// Driver Code

    let n = 1552793;
    if (validate(n))
       document.write("True");
    else
      document.write("False");

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
True
```

**有效方法:**是存储每个数字的频率，如果任何地方的频率大于数字值，则返回假，否则返回真。

## C++

```
// A C++ program to validate a number
#include<bits/stdc++.h>
using namespace std;

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
bool validate(long long int n)
{
    int count[10] = {0}; 
    while (n)
    {
        // calculate frequency of each digit
        int r = n % 10;

        // If count is already r, then
        // incrementing it would invalidate,
        // hence we return false.
        if (count[r] == r)
           return false; 

        count[r]++;
        n /= 10;
    }

    return true;
}

// driver program
int main()
{
    long long int n = 1552793;
    if (validate(n))
        cout << "True";
    else
        cout << "False";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to
// validate a number
import java.io.*;

class GFG
{

// Function to validate
// number (Check if frequency
// of a digit is less than
// the digit itself or not)
static boolean validate(long n)
{
    int count[] = new int[10] ;
    while (n > 0)
    {
        // calculate frequency
        // of each digit
        int r = (int)n % 10;

        // If count is already r,
        // then incrementing it
        // would invalidate,
        // hence we return false.
        if (count[r] == r)
        return false;

        count[r]++;
        n /= 10;
    }

    return true;
}

// Driver Code
public static void main (String[] args)
{
    long n = 1552793;
    if (validate(n))
        System.out.println("True");
    else
        System.out.println("False");
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# A Python3 program to validate a number
import math as mt

# Function to validate number (Check if
# frequency of a digit is less than the
# digit itself or not)
def validate(n):

    count = [0 for i in range(10)]
    while (n > 0):

        # calculate frequency of each digit
        r = n % 10

        # If count is already r, then
        # incrementing it would invalidate,
        # hence we return false.
        if (count[r] == r):
            return False

        count[r] += 1
        n = n // 10

    return True

# Driver Code
n = 1552793
if (validate(n)):
    print("True")
else:
    print("False")

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// A C# program to validate a number
using System;

class GFG
{
// Function to validate number
// (Check if frequency of a digit is
// less than the digit itself or not)
static bool validate(long n)
{
    int []count = new int[10] ;
    while (n > 0)
    {
        // calculate frequency
        // of each digit
        int r = (int)n % 10;

        // If count is already r, then 
        // incrementing it would invalidate,
        // hence we return false.
        if (count[r] == r)
        return false;

        count[r]++;
        n /= 10;
    }

    return true;
}

// Driver Code
static public void Main ()
{
    long n = 1552793;
    if (validate(n))
        Console.WriteLine("True");
    else
        Console.WriteLine("False");
}
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to validate a number

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
function validate($n)
{
    $count=array(10);
    while ($n)
    {
        // calculate frequency of each digit
        $r = $n % 10;

        // If count is already r, then
        // incrementing it would invalidate,
        // hence we return false.
        if (($count[$r] == $r))
        {
            return false;
        }

        $count[$r] = $count[$r] + 1;
        $n = $n / 10;
    }

    return true;
}

// Driver Code
    $n = 1552793;
    $geek = validate($n) ?"True" :"False";
    echo($geek);
?>
```

## java 描述语言

```
<script>

// A JavaScript program to validate a number

// Function to validate number (Check if
// frequency of a digit is less than the
// digit itself or not)
function validate(n)
{
    let count = new Uint8Array(10);
    while (n)
    {
        // calculate frequency of each digit
        let r = n % 10;

        // If count is already r, then
        // incrementing it would invalidate,
        // hence we return false.
        if (count[r] == r)
        return false;

        count[r]++;
        n = Math.floor(n / 10);
    }

    return true;
}

// driver program

    let n = 1552793;
    if (validate(n))
        document.write( "True");
    else
        document.write("False");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
True
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。