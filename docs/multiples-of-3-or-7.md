# 3 或 7 的倍数

> 原文:[https://www.geeksforgeeks.org/multiples-of-3-or-7/](https://www.geeksforgeeks.org/multiples-of-3-or-7/)

给定一个正整数 n，求小于等于 n 的 3 或 7 的所有倍数的计数
**例:**

```
Input : n = 10
Output : Count = 4
The multiples are 3, 6, 7 and 9

Input : n = 25
Output : Count = 10
The multiples are 3, 6, 7, 9, 12, 14, 15, 18, 21 and 24
```

一个简单的解决方案是迭代从 1 到 n 的所有数字，并且每当一个数字是 3 或 7 的倍数或者两者都是时递增计数。

## C++

```
// A Simple C++ program to find count of all
// numbers that multiples
#include<iostream>
using namespace std;

// Returns count of all numbers smaller than
// or equal to n and multiples of 3 or 7 or both
int countMultiples(int n)
{
    int res = 0;
    for (int i=1; i<=n; i++)
       if (i%3==0 || i%7 == 0)
           res++;

    return res;
}

// Driver code
int main()
{
   cout << "Count = " << countMultiples(25);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to
// find count of all numbers
// that multiples
import java.io.*;

class GFG
{

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
static int countMultiples(int n)
{
    int res = 0;
    for (int i = 1; i <= n; i++)
    if (i % 3 == 0 || i % 7 == 0)
        res++;

    return res;
}

// Driver Code
public static void main (String[] args)
{
    System.out.print("Count = ");
    System.out.println(countMultiples(25));
}
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# A Simple Python3 program to
# find count of all numbers
# that multiples

# Returns count of all numbers
# smaller than or equal to n
# and multiples of 3 or 7 or both
def countMultiples(n):
    res = 0;
    for i in range(1, n + 1):
        if (i % 3 == 0 or i % 7 == 0):
            res += 1;

    return res;

# Driver code
print("Count =", countMultiples(25));

# This code is contributed by mits
```

## C#

```
// A Simple C# program to
// find count of all numbers
// that are multiples of 3 or 7
using System;

class GFG
{

// Returns count of all 
// numbers smaller than
// or equal to n  and
// are multiples of 3 or
// 7 or both
static int countMultiples(int n)
{
    int res = 0;
    for (int i = 1; i <= n; i++)
    if (i % 3 == 0 || i % 7 == 0)
        res++;

    return res;
}

// Driver Code
static public void Main ()
{
    Console.Write("Count = ");
    Console.WriteLine(countMultiples(25));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple PHP program to find count
// of all numbers that multiples

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
function countMultiples($n)
{
    $res = 0;
    for ($i = 1; $i <= $n; $i++)
    if ($i % 3 == 0 || $i % 7 == 0)
        $res++;

    return $res;
}

// Driver code
echo "Count = " ,countMultiples(25);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// A Simple JavaScript program to find count
// of all numbers that multiples

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
function countMultiples(n)
{
    let res = 0;
    for (let i = 1; i <= n; i++)
    if (i % 3 == 0 || i % 7 == 0)
        res++;

    return res;
}

// Driver code
document.write( "Count = " +countMultiples(25));

// This code is contributed by bobby

</script>
```

**输出:**

```
Count = 10
```

**时间复杂度:** O(n)
一个高效的解决方案可以在 O(1)时间内解决上述问题。这个想法是数 3 的倍数，加上 7 的倍数，然后减去 21 的倍数，因为这些是数两次。

```
count = n/3 + n/7 - n/21 
```

## C++

```
// A better C++ program to find count of all
// numbers that multiples
#include<iostream>
using namespace std;

// Returns count of all numbers smaller than
// or equal to n and multiples of 3 or 7 or both
int countMultiples(int n)
{
   return n/3 + n/7 -n/21;
}

// Driver code
int main()
{
   cout << "Count = " << countMultiples(25);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A better Java program to
// find count of all numbers
// that multiples
import java.io.*;

class GFG
{

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
static int countMultiples(int n)
{
    return n / 3 + n / 7 - n / 21;
}

// Driver code
public static void main (String args [] )
{
    System.out.println("Count = " +
                        countMultiples(25));
}
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python 3 program to find count of
# all numbers that multiples

# Returns count of all numbers
# smaller than or equal to n and
# multiples of 3 or 7 or both
def countMultiples(n):
    return n / 3 + n / 7 - n / 21;

# Driver code
n = ((int)(countMultiples(25)));
print("Count =", n);

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// A better Java program to
// find count of all numbers
// that multiples
using System;

class GFG
{

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
static int countMultiples(int n)
{
    return n / 3 + n / 7 - n / 21;
}

// Driver Code
static public void Main ()
{
    Console.WriteLine("Count = " +
                       countMultiples(25));
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A better PHP program to find count
// of all numbers that multiples

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
function countMultiples($n)
{
return floor($n / 3 + $n / 7 - $n / 21);
}

// Driver code
echo "Count = " , countMultiples(25);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find count
// of all numbers that multiples

// Returns count of all numbers
// smaller than or equal to n
// and multiples of 3 or 7 or both
function countMultiples(n)
{
return Math.floor(n / 3 + n / 7 - n / 21);
}

// Driver code
document.write( "Count = " +countMultiples(25));

// This code is contributed by bobby

</script>
```

**输出:**

```
Count = 10
```

**时间复杂度:** O(1)
**练习:**
现在试一下在 O(1)时间内求所有小于或等于 n 的数的和以及 3 或 7 的倍数或两者的问题。
本文由**绍拉布·古普塔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。