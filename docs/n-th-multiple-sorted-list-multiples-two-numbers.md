# 两个数倍数排序列表中的第 N 个倍数

> 原文:[https://www . geesforgeks . org/n-th-multiple-sorted-list-multiples-two-numbers/](https://www.geeksforgeeks.org/n-th-multiple-sorted-list-multiples-two-numbers/)

给定三个正整数 **a、b 和 n** 。考虑一个包含“a”和“b”的所有倍数的列表。对列表进行排序，并删除重复项。任务是找到列表的第 n 个元素。
**例:**

```
Input :  a = 3, b = 5, n = 5
Output : 10
a = 3 b = 5, Multiple of 3 are 3, 6, 9, 12, 15,... and 
multiples of 5 are 5, 10, 15, 20,.... 
After deleting duplicate element and sorting:
3, 5, 6, 9, 10, 12, 15, 18, 20,.... 
The 5th element in the sequence is 10.

Input : n = 6, a = 2, b = 3 
Output : 9
```

**方法一:(蛮力)**
生成‘a’的第一个‘n’倍数。现在，生成 b 的第一个 n 倍，这样它就不属于 a 的第一个 n 倍。这可以使用二分搜索法来完成。

## C++

```
// C++ program to find n-th number in the sorted
// list of multiples of two numbers.
#include<bits/stdc++.h>
using namespace std;

// Return the n-th number in the sorted
// list of multiples of two numbers.
int nthElement(int a, int b, int n)
{
    vector<int> seq;

    // Generating first n multiple of a.
    for (int i = 1; i <= n; i++)
        seq.push_back(a*i);

    // Sorting the sequence.
    sort(seq.begin(), seq.end());

    // Generating and storing first n multiple of b
    // and storing if not present in the sequence.
    for (int i = 1, k = n; i <= n && k; i++)
    {
        // If not present in the sequence
        if (!binary_search(seq.begin(), seq.end(), b*i))
        {
            // Storing in the sequence.
            seq.push_back(b*i);

            sort(seq.begin(), seq.end());
            k--;
        }
    }

    return seq[n - 1];
}

// Driven Program
int main()
{
    int a = 3, b = 5, n = 5;
    cout << nthElement(a, b, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number
// in the sorted list of multiples
// of two numbers.
import java.io.*;
import java.util.*;
class GFG
{
// Return the n-th number in the sorted
// list of multiples of two numbers.
static int nthElement(int a, int b, int n)
{
    ArrayList<Integer> seq = new
              ArrayList<Integer>(n * n + 1);

    // Generating first n multiple of a.
    for (int i = 1; i <= n; i++)
        seq.add(a * i);

    // Sorting the sequence.
    Collections.sort(seq);

    // Generating and storing first n
    // multiple of b and storing if
    // not present in the sequence.
    for (int i = 1, k = n;
             i <= n && k > 0; i++)
    {
        // If not present in the sequence
        if (seq.indexOf(b * i) == -1)
        {
            // Storing in the sequence.
            seq.add(b * i);
            Collections.sort(seq);
            k--;
        }
    }
    return seq.get(n - 1);
}

// Driver Code
public static void main(String[] args)
{
    int a = 3, b = 5, n = 5;
    System.out.println(nthElement(a, b, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find n-th
# number in the sorted list of
# multiples of two numbers.

# Return the n-th number in the
# sorted list of multiples of
# two numbers.
def nthElement(a, b, n):
    seq = [];

    # Generating first n
    # multiple of a.
    for i in range(1, n + 1):
        seq.append(a * i);

    # Sorting the sequence.
    seq.sort();

    # Generating and storing first
    # n multiple of b and storing
    # if not present in the sequence.
    i = 1;
    k = n;
    while(i <= n and k > 0):

        # If not present in the sequence
        try:
            z = seq.index(b * i);
        except ValueError:

            # Storing in the sequence.
            seq.append(b * i);
            seq.sort();
            k -= 1;
        i += 1;

    return seq[n - 1];

# Driver Code
a = 3;
b = 5;
n = 5;
print(nthElement(a, b, n));

# This code is contributed by mits
```

## C#

```
// C# program to find n-th number
// in the sorted list of multiples
// of two numbers.
using System;
using System.Collections;

class GFG
{
// Return the n-th number in the sorted
// list of multiples of two numbers.
static int nthElement(int a,
                      int b, int n)
{
    ArrayList seq = new ArrayList();

    // Generating first n multiple of a.
    for (int i = 1; i <= n; i++)
        seq.Add(a * i);

    // Sorting the sequence.
    seq.Sort();

    // Generating and storing first n
    // multiple of b and storing if
    // not present in the sequence.
    for (int i = 1, k = n;
             i <= n && k > 0; i++)
    {
        // If not present in the sequence
        if (!seq.Contains(b * i))
        {
            // Storing in the sequence.
            seq.Add(b * i);
            seq.Sort();
            k--;
        }
    }

    return (int)seq[n - 1];
}

// Driver Code
static void Main()
{
    int a = 3, b = 5, n = 5;
    Console.WriteLine(nthElement(a, b, n));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
    // Javascript program to find n-th number
    // in the sorted list of multiples
    // of two numbers.

    // Return the n-th number in the sorted
    // list of multiples of two numbers.
    function nthElement(a, b, n)
    {
        let seq = [];

        // Generating first n multiple of a.
        for (let i = 1; i <= n; i++)
            seq.push(a * i);

        // Sorting the sequence.
        seq.sort(function(a, b){return a - b});

        // Generating and storing first n
        // multiple of b and storing if
        // not present in the sequence.
        for (let i = 1, k = n;
                 i <= n && k > 0; i++)
        {
            // If not present in the sequence
            if (!seq.includes(b * i))
            {
                // Storing in the sequence.
                seq.push(b * i);
                seq.sort(function(a, b){return a - b});
                k--;
            }
        }

        return seq[n - 1];
    }

    let a = 3, b = 5, n = 5;
    document.write(nthElement(a, b, n));

// This code is contributed by decode2207.
</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th number
// in the sorted list of multiples
// of two numbers.

// Return the n-th number in the sorted
// list of multiples of two numbers.
function nthElement($a, $b, $n)
{
    $seq = array();

    // Generating first n multiple of a.
    for ($i = 1; $i <= $n; $i++)
        array_push($seq, $a * $i);

    // Sorting the sequence.
    sort($seq);

    // Generating and storing first
    // n multiple of b and storing
    // if not present in the sequence.
    for ($i = 1, $k = $n;
         $i <= $n && $k > 0; $i++)
    {
        // If not present in the sequence
        if (array_search($b * $i, $seq) == 0)
        {
            // Storing in the sequence.
            array_push($seq, $b * $i);

            sort($seq);
            $k--;
        }
    }

    return $seq[$n - 1];
}

// Driver Code
$a = 3;
$b = 5;
$n = 5;
echo nthElement($a, $b, $n);

// This code is contributed by mits
?>
```

**输出:**

```
10
```

**方法 2:(有效方法)**
想法是利用 a 和 b 的公倍数使用 LCM(a，b)去除的事实。设 f(a，b，x)是一个计算小于 x 的数以及 a 和 b 的倍数的函数，现在，利用包含-排除原理，我们可以说，

```
f(a, b, x) :  Count of number that are less than x
              and multiples of a and b

f(a, b, x) = (x/a) + (x/b) - (x/lcm(a, b))
where (x/a) define number of multiples of a
(x/b) define number of multiple of b
(x/lcm(a, b)) define the number of common multiples 
of a and b.
```

注意，a 和 b 是常数。随着 x 的增加，f(a，b，x)也会增加。因此我们可以应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)求 x 的最小值，使得 f(a，b，x) > = n，函数的下界就是需要的答案。
第 n 项的上限是 min(a，b)*n。注意，当 a 和 b 的倍数中没有公共元素时，我们得到第 n 项的最大值。
下面是上述方法的实现:

## C++

```
// C++ program to find n-th number in thes
// sorted list of multiples of two numbers.
#include<bits/stdc++.h>
using namespace std;

// Return the Nth number in the sorted
// list of multiples of two numbers.
int nthElement(int a, int b, int n)
{
    // Finding LCM of a and b.
    int lcm = (a * b)/__gcd(a,b);

    // Binary Search.
    int l = 1, r = min(a, b)*n;
    while (l <= r)
    {
        // Finding the middle element.
        int mid = (l + r)>>1;

        // count of number that are less than
        // mid and multiples of a and b
        int val = mid/a + mid/b - mid/lcm;

        if (val == n)
            return max((mid/a)*a, (mid/b)*b);

        if (val < n)
            l = mid + 1;
        else
            r = mid - 1;
    }
}

// Driven Program
int main()
{
    int a = 5, b = 3, n = 5;
    cout << nthElement(a, b, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number in the
// sorted list of multiples of two numbers.
import java.io.*;

public class GFG{

// Recursive function to return
// gcd of a and b
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

// Return the Nth number in the sorted
// list of multiples of two numbers.
static int nthElement(int a, int b, int n)
{
    // Finding LCM of a and b.
    int lcm = (a * b) / __gcd(a, b);

    // Binary Search.
    int l = 1, r = Math.min(a, b) * n;
    while (l <= r)
    {
        // Finding the middle element.
        int mid = (l + r) >> 1;

        // count of number that are less than
        // mid and multiples of a and b
        int val = mid / a + mid / b -
                  mid / lcm;

        if (val == n)
            return Math.max((mid / a) * a,
                            (mid / b) * b);

        if (val < n)
            l = mid + 1;
        else
            r = mid - 1;
    }
    return 0;
}

// Driver Code
static public void main (String[] args)
{
    int a = 5, b = 3, n = 5;
    System.out.println(nthElement(a, b, n));
}
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find n-th number
# in thes sorted list of multiples of
# two numbers.
import math

# Return the Nth number in the sorted
# list of multiples of two numbers.
def nthElement(a, b, n):

    # Finding LCM of a and b.
    lcm = (a * b) / int(math.gcd(a, b))

    # Binary Search.
    l = 1
    r = min(a, b) * n
    while (l <= r):

        # Finding the middle element.
        mid = (l + r) >> 1

        # count of number that are less
        # than mid and multiples of a
        # and b
        val = (int(mid / a) + int(mid / b)
                         - int(mid / lcm))

        if (val == n):
            return int( max(int(mid / a) * a,
                          int(mid / b) * b) )

        if (val < n):
            l = mid + 1
        else:
            r = mid - 1

# Driven Program
a = 5
b = 3
n = 5
print(nthElement(a, b, n))

# This code is contributed by Smitha.
```

## C#

```
// C# program to find n-th number in thes
// sorted list of multiples of two numbers.
using System;

public class GFG{

// Recursive function to return
// gcd of a and b
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

// Return the Nth number in the sorted
// list of multiples of two numbers.
static int nthElement(int a, int b, int n)
{
    // Finding LCM of a and b.
    int lcm = (a * b) / __gcd(a, b);

    // Binary Search.
    int l = 1, r = Math.Min(a, b) * n;
    while (l <= r)
    {
        // Finding the middle element.
        int mid = (l + r) >> 1;

        // count of number that are less than
        // mid and multiples of a and b
        int val = mid / a + mid / b -
                  mid / lcm;

        if (val == n)
            return Math.Max((mid / a) * a,
                            (mid / b) * b);

        if (val < n)
            l = mid + 1;
        else
            r = mid - 1;
    }
    return 0;
}

// Driver Code
    static public void Main (String []args)
    {
        int a = 5, b = 3, n = 5;
            Console.WriteLine(nthElement(a, b, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th number
// in a sorted list of multiples
// of two numbers.

// function to calculate gcd
function gcd($a, $b)
{
    return ($a % $b) ?
        gcd($b, $a % $b) : $b;
}

// Return the Nth number in the sorted
// list of multiples of two numbers.
function nthElement($a, $b, $n)
{
    // Finding LCM of a and b.
    $lcm = (int)(($a * $b) / gcd($a, $b));

    // Binary Search.
    $l = 1;
    $r = min($a, $b) * $n;
    while ($l <= $r)
    {
        // Finding the middle element.
        $mid = ($l + $r) >> 1;

        // count of number that are
        // less than mid and multiples
        // of a and b
        $val = (int)($mid / $a) +
               (int)($mid / $b) -
               (int)($mid / $lcm);

        if ($val == $n)
            return max((int)(($mid / $a)) * $a,
                       (int)(($mid / $b)) * $b);

        if ($val < $n)
            $l = $mid + 1;
        else
            $r = $mid - 1;
    }
}

// Driver code
$a = 5;
$b = 3;
$n = 5;
echo nthElement($a, $b, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th number in the
// sorted list of multiples of two numbers.

// Recursive function to return
// gcd of a and b
function __gcd(a , b)
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

// Return the Nth number in the sorted
// list of multiples of two numbers.
function nthElement(a , b , n)
{
    // Finding LCM of a and b.
    var lcm = parseInt((a * b) / __gcd(a, b));

    // Binary Search.
    var l = 1, r = Math.min(a, b) * n;
    while (l <= r)
    {
        // Finding the middle element.
        var mid = (l + r) >> 1;

        // count of number that are less than
        // mid and multiples of a and b
        var val = parseInt(mid / a) + parseInt(mid / b) -
                  parseInt(mid / lcm);

        if (val == n)
            return Math.max(parseInt(mid / a) * a,
                            parseInt(mid / b) * b);

        if (val < n)
            l = mid + 1;
        else
            r = mid - 1;
    }
    return 0;
}

// Driver Code
var a = 5, b = 3, n = 5;
document.write(nthElement(a, b, n));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
10
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。