# 程序检查强号码

> 原文:[https://www . geesforgeks . org/program-to-check-strong-number/](https://www.geeksforgeeks.org/program-to-check-strong-number/)

**强数**是位数阶乘之和等于原数的数。给定一个数，检查它是否是强数。
**例:**

```
Input  : n = 145
Output : Yes
Sum of digit factorials = 1! + 4! + 5!
                        = 1 + 24 + 120
                        = 145

Input :  n = 534
Output : No
```

```
1) Initialize sum of factorials as 0\. 
2) For every digit d, do following
   a) Add d! to sum of factorials.
3) If sum factorials is same as given 
   number, return true.
4) Else return false.
```

优化是预先计算从 0 到 10 的所有数字的阶乘。

## C++

```
// C++ program to check if a number is
// strong or not.
#include <bits/stdc++.h>
using namespace std;

int f[10];

// Fills factorials of digits from 0 to 9.
void preCompute()
{
    f[0] = f[1] = 1;
    for (int i = 2; i<10; ++i)
        f[i] = f[i-1] * i;
}

// Returns true if x is Strong
bool isStrong(int x)
{
    int factSum = 0;

    // Traverse through all digits of x.
    int temp = x;
    while (temp)
    {
        factSum += f[temp%10];
        temp /= 10;
    }

    return (factSum == x);
}

// Driver code
int main()
{
    preCompute();

    int x = 145;
    isStrong(x) ? cout << "Yes\n" : cout << "No\n";
    x = 534;
    isStrong(x) ? cout << "Yes\n" : cout << "No\n";
    return 0;
}       
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a number is Strong or not

class CheckStrong
{
    static int f[] = new int[10];

    // Fills factorials of digits from 0 to 9.
    static void preCompute()
    {
        f[0] = f[1] = 1;
        for (int i = 2; i<10; ++i)
            f[i] = f[i-1] * i;
    }

    // Returns true if x is Strong
    static boolean isStrong(int x)
    {
        int factSum = 0;

        // Traverse through all digits of x.
        int temp = x;
        while (temp>0)
        {
            factSum += f[temp%10];
            temp /= 10;
        }

        return (factSum == x);
    }

    // main function
    public static void main (String[] args)
    {  
        // calling preCompute
        preCompute();

        // first pass
        int x = 145;
        if(isStrong(x))
        {
            System.out.println("Yes");
        }
        else
            System.out.println("No");

        // second pass
        x = 534;
        if(isStrong(x))
        {
            System.out.println("Yes");
        }
        else
            System.out.println("No");
    }
}
```

## 计算机编程语言

```
# Python program to check if a number is
# strong or not.

f = [None] * 10

# Fills factorials of digits from 0 to 9.
def preCompute() :
    f[0] = f[1] = 1;
    for i in range(2,10) :
        f[i] = f[i-1] * i

# Returns true if x is Strong
def isStrong(x) :

    factSum = 0
    # Traverse through all digits of x.
    temp = x
    while (temp) :
        factSum = factSum + f[temp % 10]
        temp = temp / 10

    return (factSum == x)

# Driver code
preCompute()
x = 145
if(isStrong(x) ) :
    print "Yes"
else :
    print "No"
x = 534
if(isStrong(x)) :
    print "Yes"
else:
    print "No"

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if
// a number is Strong or not
using System;

class CheckStrong
{
    static int []f = new int[10];

    // Fills factorials of digits from 0 to 9.
    static void preCompute()
    {
        f[0] = f[1] = 1;
        for (int i = 2; i < 10; ++i)
            f[i] = f[i - 1] * i;
    }

    // Returns true if x is Strong
    static bool isStrong(int x)
    {
        int factSum = 0;

        // Traverse through all digits of x.
        int temp = x;
        while (temp > 0)
        {
            factSum += f[temp % 10];
            temp /= 10;
        }

        return (factSum == x);
    }

    // Driver Code
    public static void Main ()
    {
        // calling preCompute
        preCompute();

        // first pass
        int x = 145;
        if(isStrong(x))
        {
            Console.WriteLine("Yes");
        }
        else
            Console.WriteLine("No");

        // second pass
        x = 534;
        if(isStrong(x))
        {
            Console.WriteLine("Yes");
        }
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is strong or not.

$f[10] = array();

// Fills factorials of digits
// from 0 to 9.
function preCompute()
{
    global $f;
    $f[0] = $f[1] = 1;
    for ($i = 2; $i < 10; ++$i)
        $f[$i] = $f[$i - 1] * $i;
}

// Returns true if x is Strong
function isStrong($x)
{
    global $f;
    $factSum = 0;

    // Traverse through all digits of x.
    $temp = $x;
    while ($temp)
    {
        $factSum += $f[$temp % 10];
        $temp = (int)$temp / 10;
    }

    return ($factSum == $x);
}

// Driver code
preCompute();
$x = 145;

if(isStrong(!$x))
    echo "Yes\n";
else
    echo "No\n";
$x = 534;
if(isStrong($x))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number is
// strong or not.

let f = new Array(10);

// Fills factorials of digits from 0 to 9.
function preCompute()
{
    f[0] = f[1] = 1;
    for (let i = 2; i<10; ++i)
        f[i] = f[i-1] * i;
}

// Returns true if x is Strong
function isStrong(x)
{
    let factSum = 0;

    // Traverse through all digits of x.
    let temp = x;
    while (temp)
    {
        factSum += f[temp%10];
        temp = Math.floor(temp/10);
    }

    return (factSum == x);
}

// Driver code

    preCompute();

    let x = 145;
    isStrong(x) ? document.write("Yes" + "<br>") :
    document.write("No" + "<br>");
    x = 534;
    isStrong(x) ? document.write("Yes" + "<br>") :
    document.write("No" + "<br>");

//This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Yes
No
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。