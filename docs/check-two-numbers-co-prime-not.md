# 检查两个数是否同素

> 原文:[https://www . geesforgeks . org/check-two-numbers-co-prime-not/](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)

如果两个数 A 和 B 的最大公约数为 1，则称它们为同素或互素。给了你两个数字 A 和 B，看看它们是不是同素的。
**例:**

```
Input : 2 3
Output : Co-Prime

Input : 4 8
Output : Not Co-Prime
```

## C++

```
// CPP program to check if two
// numbers are co-prime or not
#include<bits/stdc++.h>
using namespace std;

// function to check and print if
// two numbers are co-prime or not
void coprime(int a, int b) {

    if ( __gcd(a, b) == 1)
        cout << "Co-Prime" << endl;
    else
        cout << "Not Co-Prime" << endl;       
}

// driver code
int main()
{
    int a = 5, b = 6;
    coprime(a, b);   
    a = 8, b = 16;
    coprime(a, b);       
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two
// numbers are co-prime or not
class GFG {

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);

        return __gcd(a, b-a);
    }

    // function to check and print if
    // two numbers are co-prime or not
    static void coprime(int a, int b) {

        if ( __gcd(a, b) == 1)
            System.out.println("Co-Prime");
        else
            System.out.println("Not Co-Prime");    
    }

    //driver code
    public static void main (String[] args)
    {
        int a = 5, b = 6;
        coprime(a, b);

        a = 8; b = 16;
        coprime(a, b);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if two
# numbers are co-prime or not

# Recursive function to
# return gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0): return 0

    # base case
    if (a == b): return a

    # a is greater
    if (a > b):
        return __gcd(a - b, b)

    return __gcd(a, b - a)

# Function to check and print if
# two numbers are co-prime or not
def coprime(a, b):

    if ( __gcd(a, b) == 1):
        print("Co-Prime")
    else:
        print("Not Co-Prime")    

# Driver code
a = 5; b = 6
coprime(a, b)

a = 8; b = 16
coprime(a, b)

# This code is contributed by Anant Agarwal
```

## C#

```
// C# program to check if two
// numbers are co-prime or not
using System;

class GFG {

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);

        return __gcd(a, b - a);
    }

    // function to check and print if
    // two numbers are co-prime or not
    static void coprime(int a, int b) {

        if (__gcd(a, b) == 1)
            Console.WriteLine("Co-Prime");
        else
            Console.WriteLine("Not Co-Prime");
    }

    // Driver code
    public static void Main()
    {
        int a = 5, b = 6;
        coprime(a, b);
        a = 8;
        b = 16;
        coprime(a, b);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if two
// numbers are co-prime or not

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
    {
        // Everything divides 0
        if ($a == 0 || $b == 0)
            return 0;

        // base case
        if ($a == $b)
            return $a;

        // a is greater
        if ($a > $b)
            return __gcd($a - $b, $b);

        return __gcd($a, $b - $a);
    }

    // function to check and print if
    // two numbers are co-prime or not
function coprime($a, $b)
{
    if (__gcd($a, $b) == 1)
        echo "Co-Prime","\n";
    else
        echo "Not Co-Prime","\n";
}

// Driver Code
$a = 5; $b = 6;
coprime($a, $b);
$a = 8;
$b = 16;
coprime($a, $b);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to check if two
// numbers are co-prime or not

// Recursive function to
// return gcd of a and b
function __gcd(a, b)
{

    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Function to check and print if
// two numbers are co-prime or not
function coprime(a, b)
{
    if (__gcd(a, b) == 1)
        document.write("Co-Prime" + "<br>");
    else
        document.write("Not Co-Prime");    
}

// Driver Code
var a = 5, b = 6;
coprime(a, b);

a = 8; b = 16;
coprime(a, b);

// This code is contributed by Kirti

</script>
```

**输出:**

```
Co-Prime
Not Co-Prime
```

本文由 [**迪本杜·罗伊·乔杜里**](https://auth.geeksforgeeks.org/profile.php?user=Dibyendu Roy Chaudhuri) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。