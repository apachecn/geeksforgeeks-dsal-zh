# 从 1 到 n，以 4 为数字计数

> 原文:[https://www . geesforgeks . org/count-numbers-from-1-n-the-has-4-as-a-digits/](https://www.geeksforgeeks.org/count-numbers-from-1-to-n-that-have-4-as-a-a-digit/)

给定一个数字 n，找出从 1 到 n 的所有数字的计数，其中 4 是一个数字。
**例:**

```
Input:   n = 5
Output:  1
Only 4 has '4' as digit

Input:   n = 50
Output:  14

Input:   n = 328
Output:  60
```

这个问题主要是上一篇关于[计算所有数字从 1 到 n 的数字之和](https://www.geeksforgeeks.org/count-sum-of-digits-in-numbers-from-1-to-n/)的一个变种。

**天真解决方案:**
天真解决方案是从 1 到 n 遍历每个数字 x，检查 x 是否有 4。为了检查 x 是否有，我们可以遍历 x 的所有数字。下面是上述思想的实现:

## C++

```
// A Simple C++ program to compute sum of digits in numbers from 1 to n
#include<iostream>
using namespace std;

bool has4(int x);

// Returns sum of all digits in numbers from 1 to n
int countNumbersWith4(int n)
{
    int result = 0; // initialize result

    // One by one compute sum of digits in every number from
    // 1 to n
    for (int x=1; x<=n; x++)
        result += has4(x)? 1 : 0;

    return result;
}

// A utility function to compute sum of digits in a
// given number x
bool has4(int x)
{
    while (x != 0)
    {
        if (x%10 == 4)
           return true;
        x   = x /10;
    }
    return false;
}

// Driver Program
int main()
{
   int n = 328;
   cout << "Count of numbers from 1 to " << n
        << " that have 4 as a a digit is "
        << countNumbersWith4(n) << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute sum of
// digits in numbers from 1 to n
import java.io.*;

class GFG {

    // Returns sum of all digits
    // in numbers from 1 to n
    static int countNumbersWith4(int n)
    {
        // initialize result
        int result = 0;

        // One by one compute sum of digits
        // in every number from 1 to n
        for (int x=1; x<=n; x++)
            result += has4(x)? 1 : 0;

        return result;
    }

    // A utility function to compute sum
    // of digits in a given number x
    static boolean has4(int x)
    {
        while (x != 0)
        {
            if (x%10 == 4)
               return true;
            x   = x /10;
        }
        return false;
    }

    // Driver Program
    public static void main(String args[])
    {
       int n = 328;
       System.out.println("Count of numbers from 1 to "
                          + " that have 4 as a a digit is "
                          + countNumbersWith4(n)) ;
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# A Simple Python 3 program to compute
# sum of digits in numbers from 1 to n

# Returns sum of all digits in numbers from 1 to n
def countNumbersWith4(n) :
    result = 0 # initialize result

    # One by one compute sum of digits
    # in every number from 1 to n
    for x in range(1, n + 1) :
        if(has4(x) == True) :
            result = result + 1

    return result

# A utility function to compute sum 
# of digits in a given number x
def has4(x) :
    while (x != 0) :
        if (x%10 == 4) :
            return True
        x = x //10

    return False

# Driver Program
n = 328
print ("Count of numbers from 1 to ", n,
        " that have 4 as a a digit is ",
                    countNumbersWith4(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to compute sum of
// digits in numbers from 1 to n
using System;

public class GFG
{

    // Returns sum of all digits
    // in numbers from 1 to n
    static int countNumbersWith4(int n)
    {

        // initialize result
        int result = 0;

        // One by one compute sum of digits
        // in every number from 1 to n
        for (int x = 1; x <= n; x++)
            result += has4(x) ? 1 : 0;

        return result;
    }

    // A utility function to compute sum
    // of digits in a given number x
    static bool has4(int x)
    {
        while (x != 0)
        {
            if (x % 10 == 4)
            return true;
            x = x / 10;
        }
        return false;
    }

    // Driver Code
    public static void Main()
    {
        int n = 328;
        Console.WriteLine("Count of numbers from 1 to "
                        + " that have 4 as a a digit is "
                        + countNumbersWith4(n)) ;
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute sum of
// digits in numbers from 1 to n

// Returns sum of all digits
// in numbers from 1 to n
function countNumbersWith4($n)
{
    $result = 0; // initialize result

    // One by one compute sum of
    // digits in every number from 1 to n
    for ($x = 1; $x <= $n; $x++)
        $result += has4($x) ? 1 : 0;

    return $result;
}

// A utility function to compute
// sum of digits in a given number x
function has4($x)
{
    while ($x != 0)
    {
        if ($x % 10 == 4)
        return true;
        $x = intval($x / 10);
    }
    return false;
}

// Driver Code
$n = 328;
echo "Count of numbers from 1 to " . $n .
        " that have 4 as a a digit is " .
                   countNumbersWith4($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to compute sum of
// digits in numbers from 1 to n

// Returns sum of all digits
// in numbers from 1 to n
function countNumbersWith4(n)
{

    // Initialize result
    let result = 0;

    // One by one compute sum of digits
    // in every number from 1 to n
    for(let x = 1; x <= n; x++)
        result += has4(x) ? 1 : 0;

    return result;
}

// A utility function to compute sum
// of digits in a given number x
function has4(x)
{
    while (x != 0)
    {
        if (x % 10 == 4)
           return true;

        x = Math.floor(x / 10);
    }
    return false;
}

// Driver code
let n = 328;
document.write("Count of numbers from 1 to " + n +
               " that have 4 as a a digit is " +
               countNumbersWith4(n)) ;

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Count of numbers from 1 to 328 that have 4 as a a digit is 60
```

**高效解决方案:**
以上是一个幼稚的解决方案。通过找到一种模式，我们可以更有效地做到这一点。
我们举几个例子。

```
Count of numbers from 0 to 9   = 1
Count of numbers from 0 to 99  = 1*9 + 10 = 19
Count of numbers from 0 to 999 = 19*9 + 100 = 271 

In general, we can write 
   count(10d) =   9 * count(10d - 1) + 10d - 1
```

在下面的实现中，上面的公式是使用[动态规划](https://www.geeksforgeeks.org/tag/dynamic-programming/)实现的，因为有重叠的子问题。
上述公式是这个想法的一个核心步骤。下面是完整的算法。

```
1) Find number of digits minus one in n. Let this value be 'd'.  
   For 328, d is 2.

2) Compute some of digits in numbers from 1 to 10d - 1\.  
   Let this sum be w. For 328, we compute sum of digits from 1 to 
   99 using above formula.

3) Find Most significant digit (msd) in n. For 328, msd is 3.

4.a) If MSD is 4\. For example if n = 428, then count of
     numbers is sum of following.
     1) Count of numbers from 1 to 399
     2) Count of numbers from 400 to 428 which is 29.

4.b) IF MSD > 4\. For example if n is 728, then count of
     numbers is sum of following.
     1) Count of numbers from 1 to 399 and count of numbers
        from 500 to 699, i.e., "a[2] * 6"
     2) Count of numbers from 400 to 499, i.e. 100
     3) Count of numbers from 700 to 728, recur for 28
4.c) IF MSD < 4\. For example if n is 328, then count of
     numbers is sum of following.
     1) Count of numbers from 1 to 299 a
     2) Count of numbers from 300 to 328, recur for 28 
```

下面是上述算法的实现。

## C++

```
// C++ program to count numbers having 4 as a digit
#include<bits/stdc++.h>
using namespace std;

// Function to count numbers from 1 to n that have
// 4 as a digit
int countNumbersWith4(int n)
{
    // Base case
   if (n < 4)
      return 0;

   // d = number of digits minus one in n. For 328, d is 2
   int d = log10(n);

   // computing count of numbers from 1 to 10^d-1,
   // d=0 a[0] = 0;
   // d=1 a[1] = count of numbers from 0 to 9 = 1
   // d=2 a[2] = count of numbers from 0 to 99 = a[1]*9 + 10 = 19
   // d=3 a[3] = count of numbers from 0 to 999 = a[2]*19 + 100 = 171
   int *a = new int[d+1];
   a[0] = 0, a[1] = 1;
   for (int i=2; i<=d; i++)
      a[i] = a[i-1]*9 + ceil(pow(10,i-1));

   // Computing 10^d
   int p = ceil(pow(10, d));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be obtained using 328/100
   int msd = n/p;

   // If MSD is 4\. For example if n = 428, then count of
   // numbers is sum of following.
   // 1) Count of numbers from 1 to 399
   // 2) Count of numbers from 400 to 428 which is 29.
   if (msd == 4)
      return (msd)*a[d] + (n%p) + 1;

   // IF MSD > 4\. For example if n is 728, then count of
   // numbers is sum of following.
   // 1) Count of numbers from 1 to 399 and count of numbers
   //    from 500 to 699, i.e., "a[2] * 6"
   // 2) Count of numbers from 400 to 499, i.e. 100
   // 3) Count of numbers from 700 to 728, recur for 28
   if (msd > 4)
      return (msd-1)*a[d] + p + countNumbersWith4(n%p);

   // IF MSD < 4\. For example if n is 328, then count of
   // numbers is sum of following.
   // 1) Count of numbers from 1 to 299 a
   // 2) Count of numbers from 300 to 328, recur for 28
   return (msd)*a[d] + countNumbersWith4(n%p);
}

// Driver Program
int main()
{
   int n = 328;
   cout << "Count of numbers from 1 to " << n
        << " that have 4 as a a digit is "
        << countNumbersWith4(n) << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers having 4 as a digit
class GFG
{

// Function to count numbers from
// 1 to n that have 4 as a digit
static int countNumbersWith4(int n)
{
    // Base case
    if (n < 4)
        return 0;

    // d = number of digits minus
    // one in n. For 328, d is 2
    int d = (int)Math.log10(n);

    // computing count of numbers from 1 to 10^d-1,
    // d=0 a[0] = 0;
    // d=1 a[1] = count of numbers from
    // 0 to 9 = 1
    // d=2 a[2] = count of numbers from
    // 0 to 99 = a[1]*9 + 10 = 19
    // d=3 a[3] = count of numbers from
    // 0 to 999 = a[2]*19 + 100 = 171
    int[] a = new int[d + 2];
    a[0] = 0;
    a[1] = 1;

    for (int i = 2; i <= d; i++)
        a[i] = a[i - 1] * 9 + (int)Math.ceil(Math.pow(10, i - 1));

    // Computing 10^d
    int p = (int)Math.ceil(Math.pow(10, d));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be obtained using 328/100
    int msd = n / p;

    // If MSD is 4\. For example if n = 428, then count of
    // numbers is sum of following.
    // 1) Count of numbers from 1 to 399
    // 2) Count of numbers from 400 to 428 which is 29.
    if (msd == 4)
        return (msd) * a[d] + (n % p) + 1;

    // IF MSD > 4\. For example if n
    // is 728, then count of numbers
    // is sum of following.
    // 1) Count of numbers from 1 to
    // 399 and count of numbers from
    // 500 to 699, i.e., "a[2] * 6"
    // 2) Count of numbers from 400
    // to 499, i.e. 100
    // 3) Count of numbers from 700 to
    // 728, recur for 28
    if (msd > 4)
        return (msd - 1) * a[d] + p +
                countNumbersWith4(n % p);

    // IF MSD < 4\. For example if n is 328, then count of
    // numbers is sum of following.
    // 1) Count of numbers from 1 to 299 a
    // 2) Count of numbers from 300 to 328, recur for 28
    return (msd) * a[d] + countNumbersWith4(n % p);
}

// Driver code
public static void main (String[] args)
{
    int n = 328;
    System.out.println("Count of numbers from 1 to "+ n +
            " that have 4 as a digit is " + countNumbersWith4(n));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to count numbers having 4 as a digit
import math as mt

# Function to count numbers from 1 to n
# that have 4 as a digit
def countNumbersWith4(n):

    # Base case
    if (n < 4):
        return 0

    # d = number of digits minus one in n.
    # For 328, d is 2
    d = int(mt.log10(n))

    # computing count of numbers from 1 to 10^d-1,
    # d=0 a[0] = 0
    # d=1 a[1] = count of numbers from 0 to 9 = 1
    # d=2 a[2] = count of numbers from
    #            0 to 99 = a[1]*9 + 10 = 19
    # d=3 a[3] = count of numbers from
    #            0 to 999 = a[2]*19 + 100 = 171
    a = [1 for i in range(d + 1)]
    a[0] = 0
    if len(a) > 1:
        a[1] = 1
    for i in range(2, d + 1):
        a[i] = a[i - 1] * 9 + mt.ceil(pow(10, i - 1))

    # Computing 10^d
    p = mt.ceil(pow(10, d))

    # Most significant digit (msd) of n,
    # For 328, msd is 3 which can be
    # obtained using 328/100
    msd = n // p

    # If MSD is 4\. For example if n = 428,
    # then count of numbers is sum of following.
    # 1) Count of numbers from 1 to 399
    # 2) Count of numbers from 400 to 428 which is 29.
    if (msd == 4):
        return (msd) * a[d] + (n % p) + 1

    # IF MSD > 4\. For example if n is 728,
    # then count of numbers is sum of following.
    # 1) Count of numbers from 1 to 399 and count
    #  of numbers from 500 to 699, i.e., "a[2] * 6"
    # 2) Count of numbers from 400 to 499, i.e. 100
    # 3) Count of numbers from 700 to 728, recur for 28
    if (msd > 4):
        return ((msd - 1) * a[d] + p +
                 countNumbersWith4(n % p))

    # IF MSD < 4\. For example if n is 328,
    # then count of numbers is sum of following.
    # 1) Count of numbers from 1 to 299 a
    # 2) Count of numbers from 300 to 328, recur for 28
    return (msd) * a[d] + countNumbersWith4(n % p)

# Driver Code
n = 328
print("Count of numbers from 1 to", n,
      "that have 4 as a digit is", countNumbersWith4(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count numbers having 4 as a digit
using System;

class GFG
{
// Function to count numbers from
//  1 to n that have 4 as a digit
static int countNumbersWith4(int n)
{
    // Base case
    if (n < 4)
        return 0;

    // d = number of digits minus
    // one in n. For 328, d is 2
    int d = (int)Math.Log10(n);

    // computing count of numbers from 1 to 10^d-1,
    // d=0 a[0] = 0;
    // d=1 a[1] = count of numbers from
    // 0 to 9 = 1
    // d=2 a[2] = count of numbers from
    // 0 to 99 = a[1]*9 + 10 = 19
    // d=3 a[3] = count of numbers from
    // 0 to 999 = a[2]*19 + 100 = 171
    int[] a = new int[d+2];
    a[0] = 0;
    a[1] = 1;

    for (int i = 2; i <= d; i++)
        a[i] = a[i - 1] * 9 + (int)Math.Ceiling(Math.Pow(10, i - 1));

    // Computing 10^d
    int p = (int)Math.Ceiling(Math.Pow(10, d));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be obtained using 328/100
    int msd = n / p;

    // If MSD is 4\. For example if n = 428, then count of
    // numbers is sum of following.
    // 1) Count of numbers from 1 to 399
    // 2) Count of numbers from 400 to 428 which is 29.
    if (msd == 4)
        return (msd) * a[d] + (n % p) + 1;

    // IF MSD > 4\. For example if n is 728, then count of
    // numbers is sum of following.
    // 1) Count of numbers from 1 to 399 and count of numbers
    // from 500 to 699, i.e., "a[2] * 6"
    // 2) Count of numbers from 400 to 499, i.e. 100
    // 3) Count of numbers from 700 to 728, recur for 28
    if (msd > 4)
        return (msd - 1) * a[d] + p + countNumbersWith4(n % p);

    // IF MSD < 4\. For example if n is 328, then count of
    // numbers is sum of following.
    // 1) Count of numbers from 1 to 299 a
    // 2) Count of numbers from 300 to 328, recur for 28
    return (msd) * a[d] + countNumbersWith4(n % p);
}

// Driver code
static void Main()
{
    int n = 328;
    Console.WriteLine("Count of numbers from 1 to "+ n +
            " that have 4 as a digit is " + countNumbersWith4(n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers having
// 4 as a digit

// Function to count numbers from 1 to n
// that have 4 as a digit
function countNumbersWith4($n)
{
    // Base case
    if ($n < 4)
        return 0;

    // d = number of digits minus one in n.
    // For 328, d is 2
    $d = (int)log10($n);

    // computing count of numbers from 1 to 10^d-1,
    // d=0 a[0] = 0;
    // d=1 a[1] = count of numbers from 0 to 9 is 1
    // d=2 a[2] = count of numbers from 0 to 99 is
    //                            a[1]*9 + 10 = 19
    // d=3 a[3] = count of numbers from 0 to 999 is
    //                          a[2]*19 + 100 = 171
    $a = array_fill(0, $d + 1, NULL);
    $a[0] = 0;
    $a[1] = 1;
    for ($i = 2; $i <= $d; $i++)
        $a[$i] = $a[$i - 1] * 9 +
                 ceil(pow(10, $i - 1));

    // Computing 10^d
    $p = ceil(pow(10, $d));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be
    // obtained using 328/100
    $msd = intval($n / $p);

    // If MSD is 4\. For example if n = 428,
    // then count of numbers is sum of following.
    // 1) Count of numbers from 1 to 399
    // 2) Count of numbers from 400 to 428 which is 29.
    if ($msd == 4)
        return ($msd) * $a[$d] + ($n % $p) + 1;

    // IF MSD > 4\. For example if n is 728,
    // then count of numbers is sum of following.
    // 1) Count of numbers from 1 to 399 and
    // count of numbers from 500 to 699, i.e., "a[2] * 6"
    // 2) Count of numbers from 400 to 499, i.e. 100
    // 3) Count of numbers from 700 to 728, recur for 28
    if ($msd > 4)
        return ($msd - 1) * $a[$d] + $p +
                countNumbersWith4($n % $p);

    // IF MSD < 4\. For example if n is 328, then
    // count of numbers is sum of following.
    // 1) Count of numbers from 1 to 299 a
    // 2) Count of numbers from 300 to 328, recur for 28
    return ($msd) * $a[$d] +
            countNumbersWith4($n % $p);
}

// Driver Code
$n = 328;
echo "Count of numbers from 1 to " . $n .
     " that have 4 as a digit is " .
      countNumbersWith4($n) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to count numbers having 4 as a digit

    // Function to count numbers from
    // 1 to n that have 4 as a digit
    function countNumbersWith4(n)
    {

        // Base case
        if (n < 4)
            return 0;

        // d = number of digits minus
        // one in n. For 328, d is 2
        let d = Math.floor(Math.log10(n));

        // computing count of numbers from 1 to 10^d-1,
        // d=0 a[0] = 0;
        // d=1 a[1] = count of numbers from
        // 0 to 9 = 1
        // d=2 a[2] = count of numbers from
        // 0 to 99 = a[1]*9 + 10 = 19
        // d=3 a[3] = count of numbers from
        // 0 to 999 = a[2]*19 + 100 = 171
        let a = new Array(d + 2);
        for(let i=0;i<d+2;i++)
        {
            a[i]=0;
        }
        a[0] = 0;
        a[1] = 1;

        for (let i = 2; i <= d; i++)
            a[i] = a[i - 1] * 9 + Math.floor(Math.ceil(Math.pow(10, i - 1)));

        // Computing 10^d
        let p = Math.floor(Math.ceil(Math.pow(10, d)));

        // Most significant digit (msd) of n,
        // For 328, msd is 3 which can be obtained using 328/100
        let msd = Math.floor(n / p);

        // If MSD is 4\. For example if n = 428, then count of
        // numbers is sum of following.
        // 1) Count of numbers from 1 to 399
        // 2) Count of numbers from 400 to 428 which is 29.
        if (msd == 4)
            return (msd) * a[d] + (n % p) + 1;

        // IF MSD > 4\. For example if n
        // is 728, then count of numbers
        // is sum of following.
        // 1) Count of numbers from 1 to
        // 399 and count of numbers from
        // 500 to 699, i.e., "a[2] * 6"
        // 2) Count of numbers from 400
        // to 499, i.e. 100
        // 3) Count of numbers from 700 to
        // 728, recur for 28
        if (msd > 4)
            return (msd - 1) * a[d] + p +
                    countNumbersWith4(n % p);

        // IF MSD < 4\. For example if n is 328, then count of
        // numbers is sum of following.
        // 1) Count of numbers from 1 to 299 a
        // 2) Count of numbers from 300 to 328, recur for 28
        return (msd) * a[d] + countNumbersWith4(n % p);
    }

    // Driver code
    let n = 328;
    document.write("Count of numbers from 1 to "+ n +
            " that have 4 as a digit is " + countNumbersWith4(n));

    //  This code is contributed by rag2127
</script>
```

**输出:**

```
Count of numbers from 1 to 328 that have 4 as a a digit is 60
```

本文由**希瓦姆**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息