# 小于给定数 n 的最近素数

> 原文:[https://www . geesforgeks . org/最近-质数-无给定数-n/](https://www.geeksforgeeks.org/nearest-prime-less-given-number-n/)

给你一个数字 n ( 3 <= n < 10^6)，你必须找到最近的小于 n 的素数？

**示例:**

```
Input : n = 10
Output: 7

Input : n = 17
Output: 13

Input : n = 30
Output: 29 
```

这个问题的一个**简单解决方案**是从 n-1 迭代到 2，对于每个数字，[检查它是否是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果是质数，则返回并打破循环。如果只有一个查询，这个解决方案看起来很好。但是如果对不同的 n 值有多个查询，则效率不高。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return nearest prime number
int prime(int n)
{

    // All prime numbers are odd except two
    if (n & 1)
        n -= 2;
    else
        n--;

    int i, j;
    for (i = n; i >= 2; i -= 2) {
        if (i % 2 == 0)
            continue;
        for (j = 3; j <= sqrt(i); j += 2) {
            if (i % j == 0)
                break;
        }
        if (j > sqrt(i))
            return i;
    }

    // It will only be executed when n is 3
    return 2;
}

// Driver Code
int main()
{
    int n = 17;
    cout << prime(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to return nearest prime number
    static int prime(int n)
    {

        // All prime numbers are odd except two
        if (n % 2 != 0)
            n -= 2;
        else
            n--;

        int i, j;
        for (i = n; i >= 2; i -= 2) {
            if (i % 2 == 0)
                continue;
            for (j = 3; j <= Math.sqrt(i); j += 2) {
                if (i % j == 0)
                    break;
            }
            if (j > Math.sqrt(i))
                return i;
        }

        // It will only be executed when n is 3
        return 2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 17;
        System.out.print(prime(n));
    }
}

// This code is contributed by subham348.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to return nearest prime number
    static int prime(int n)
    {

        // All prime numbers are odd except two
        if (n % 2 != 0)
            n -= 2;
        else
            n--;

        int i, j;
        for (i = n; i >= 2; i -= 2) {
            if (i % 2 == 0)
                continue;
            for (j = 3; j <= Math.Sqrt(i); j += 2) {
                if (i % j == 0)
                    break;
            }
            if (j > Math.Sqrt(i))
                return i;
        }

        // It will only be executed when n is 3
        return 2;
    }

    // Driver Code
    public static void Main()
    {
        int n = 17;
        Console.Write(prime(n));
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return nearest prime number
function prime(n)
{

    // All prime numbers are odd except two
    if (n & 1)
        n -= 2;
    else
        n--;

    let i, j;
    for(i = n; i >= 2; i -= 2)
    {
        if (i % 2 == 0)
            continue;
        for(j = 3; j <= Math.sqrt(i); j += 2)
        {
            if (i % j == 0)
                break;
        }
        if (j > Math.sqrt(i))
            return i;
    }

    // It will only be executed when n is 3
    return 2;
}

// Driver Code
let n = 17;

document.write(prime(n));

// This code is contributed by souravmahato348

</script>
```

**Output**

```
13
```

这个问题的一个有效解决方案是使用 Sundaram 的[筛](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)生成所有小于 10^6 的素数，然后以递增的顺序存储在数组中。现在应用修改后的[二分搜索法](http://geeksquiz.com/binary-search/)搜索最近的小于 n 的素数，这个解的时间复杂度是 O(n log n + log n) = O(n log n)。

## C++

```
// C++ program to find the nearest prime to n.
#include<bits/stdc++.h>
#define MAX 1000000
using namespace std;

// array to store all primes less than 10^6
vector<int> primes;

// Utility function of Sieve of Sundaram
void Sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram, produces primes
    // smaller than (2*x + 2) for a number given
    // number x
    int nNew = sqrt(n);

    // This array is used to separate numbers of the
    // form i+j+2ij from others where  1 <= i <= j
    int marked[n/2+500] = {0};

    // eliminate indexes which does not produce primes
    for (int i=1; i<=(nNew-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=n/2; j=j+2*i+1)
            marked[j] = 1;

    // Since 2 is a prime number
    primes.push_back(2);

    // Remaining primes are of the form 2*i + 1 such
    // that marked[i] is false.
    for (int i=1; i<=n/2; i++)
        if (marked[i] == 0)
            primes.push_back(2*i + 1);
}

// modified binary search to find nearest prime less than N
int binarySearch(int left,int right,int n)
{
    if (left<=right)
    {
        int mid = (left + right)/2;

        // base condition is, if we are reaching at left
        // corner or right corner of primes[] array then
        // return that corner element because before or
        // after that we don't have any prime number in
        // primes array
        if (mid == 0 || mid == primes.size()-1)
            return primes[mid];

        // now if n is itself a prime so it will be present
        // in primes array and here we have to find nearest
        // prime less than n so we will return primes[mid-1]
        if (primes[mid] == n)
            return primes[mid-1];

        // now if primes[mid]<n and primes[mid+1]>n that
        // mean we reached at nearest prime
        if (primes[mid] < n && primes[mid+1] > n)
            return primes[mid];
        if (n < primes[mid])
            return binarySearch(left, mid-1, n);
        else
            return binarySearch(mid+1, right, n);
    }
    return 0;
}

// Driver program to run the case
int main()
{
    Sieve();
    int n = 17;
    cout << binarySearch(0, primes.size()-1, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the nearest prime to n.
import java.util.*;

class GFG
{

static int MAX=1000000;

// array to store all primes less than 10^6
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Utility function of Sieve of Sundaram
static void Sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram, produces primes
    // smaller than (2*x + 2) for a number given
    // number x
    int nNew = (int)Math.sqrt(n);

    // This array is used to separate numbers of the
    // form i+j+2ij from others where 1 <= i <= j
    int[] marked = new int[n / 2 + 500];

    // eliminate indexes which does not produce primes
    for (int i = 1; i <= (nNew - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
                j <= n / 2; j = j + 2 * i + 1)
            marked[j] = 1;

    // Since 2 is a prime number
    primes.add(2);

    // Remaining primes are of the form 2*i + 1 such
    // that marked[i] is false.
    for (int i = 1; i <= n / 2; i++)
        if (marked[i] == 0)
            primes.add(2 * i + 1);
}

// modified binary search to find nearest prime less than N
static int binarySearch(int left,int right,int n)
{
    if (left <= right)
    {
        int mid = (left + right) / 2;

        // base condition is, if we are reaching at left
        // corner or right corner of primes[] array then
        // return that corner element because before or
        // after that we don't have any prime number in
        // primes array
        if (mid == 0 || mid == primes.size() - 1)
            return primes.get(mid);

        // now if n is itself a prime so it will be present
        // in primes array and here we have to find nearest
        // prime less than n so we will return primes[mid-1]
        if (primes.get(mid) == n)
            return primes.get(mid - 1);

        // now if primes[mid]<n and primes[mid+1]>n that
        // mean we reached at nearest prime
        if (primes.get(mid) < n && primes.get(mid + 1) > n)
            return primes.get(mid);
        if (n < primes.get(mid))
            return binarySearch(left, mid - 1, n);
        else
            return binarySearch(mid + 1, right, n);
    }
    return 0;
}

// Driver code
public static void main (String[] args)
{
    Sieve();
    int n = 17;
    System.out.println(binarySearch(0,
                        primes.size() - 1, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find the nearest
# prime to n.
import math
MAX = 10000;

# array to store all primes less
# than 10^6
primes = [];

# Utility function of Sieve of Sundaram
def Sieve():

    n = MAX;

    # In general Sieve of Sundaram, produces
    # primes smaller than (2*x + 2) for a
    # number given number x
    nNew = int(math.sqrt(n));

    # This array is used to separate numbers
    # of the form i+j+2ij from others where
    # 1 <= i <= j
    marked = [0] * (int(n / 2 + 500));

    # eliminate indexes which does not
    # produce primes
    for i in range(1, int((nNew - 1) / 2) + 1):
        for j in range(((i * (i + 1)) << 1),
                        (int(n / 2) + 1), (2 * i + 1)):
            marked[j] = 1;

    # Since 2 is a prime number
    primes.append(2);

    # Remaining primes are of the form
    # 2*i + 1 such that marked[i] is false.
    for i in range(1, int(n / 2) + 1):
        if (marked[i] == 0):
            primes.append(2 * i + 1);

# modified binary search to find nearest
# prime less than N
def binarySearch(left, right, n):
    if (left <= right):
        mid = int((left + right) / 2);

        # base condition is, if we are reaching
        # at left corner or right corner of
        # primes[] array then return that corner
        # element because before or after that
        # we don't have any prime number in
        # primes array
        if (mid == 0 or mid == len(primes) - 1):
            return primes[mid];

        # now if n is itself a prime so it will
        # be present in primes array and here
        # we have to find nearest prime less than
        # n so we will return primes[mid-1]
        if (primes[mid] == n):
            return primes[mid - 1];

        # now if primes[mid]<n and primes[mid+1]>n
        # that means we reached at nearest prime
        if (primes[mid] < n and primes[mid + 1] > n):
            return primes[mid];
        if (n < primes[mid]):
            return binarySearch(left, mid - 1, n);
        else:
            return binarySearch(mid + 1, right, n);

    return 0;

# Driver Code
Sieve();
n = 17;
print(binarySearch(0, len(primes) - 1, n));

# This code is contributed by chandan_jnu
```

## C#

```
// C# program to find the nearest prime to n.
using System;
using System.Collections;
class GFG
{

static int MAX = 1000000;

// array to store all primes less than 10^6
static ArrayList primes = new ArrayList();

// Utility function of Sieve of Sundaram
static void Sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x
    int nNew = (int)Math.Sqrt(n);

    // This array is used to separate numbers of the
    // form i+j+2ij from others where 1 <= i <= j
    int[] marked = new int[n / 2 + 500];

    // eliminate indexes which does not produce primes
    for (int i = 1; i <= (nNew - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
                 j <= n / 2; j = j + 2 * i + 1)
            marked[j] = 1;

    // Since 2 is a prime number
    primes.Add(2);

    // Remaining primes are of the form 2*i + 1
    // such that marked[i] is false.
    for (int i = 1; i <= n / 2; i++)
        if (marked[i] == 0)
            primes.Add(2 * i + 1);
}

// modified binary search to find
// nearest prime less than N
static int binarySearch(int left, int right, int n)
{
    if (left <= right)
    {
        int mid = (left + right) / 2;

        // base condition is, if we are reaching at left
        // corner or right corner of primes[] array then
        // return that corner element because before or
        // after that we don't have any prime number in
        // primes array
        if (mid == 0 || mid == primes.Count - 1)
            return (int)primes[mid];

        // now if n is itself a prime so it will be
        // present in primes array and here we have
        // to find nearest prime less than n so we
        // will return primes[mid-1]
        if ((int)primes[mid] == n)
            return (int)primes[mid - 1];

        // now if primes[mid]<n and primes[mid+1]>n
        // that mean we reached at nearest prime
        if ((int)primes[mid] < n &&
            (int)primes[mid + 1] > n)
            return (int)primes[mid];
        if (n < (int)primes[mid])
            return binarySearch(left, mid - 1, n);
        else
            return binarySearch(mid + 1, right, n);
    }
    return 0;
}

// Driver code
static void Main()
{
    Sieve();
    int n = 17;
    Console.WriteLine(binarySearch(0,
                      primes.Count - 1, n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the nearest
// prime to n.

$MAX = 10000;

// array to store all primes less
// than 10^6
$primes = array();

// Utility function of Sieve of Sundaram
function Sieve()
{
    global $MAX, $primes;
    $n = $MAX;

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x
    $nNew = (int)(sqrt($n));

    // This array is used to separate numbers
    // of the form i+j+2ij from others where
    // 1 <= i <= j
    $marked = array_fill(0, (int)($n / 2 + 500), 0);

    // eliminate indexes which does not
    // produce primes
    for ($i = 1; $i <= ($nNew - 1) / 2; $i++)
        for ($j = ($i * ($i + 1)) << 1;
             $j <= $n / 2; $j = $j + 2 * $i + 1)
            $marked[$j] = 1;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Remaining primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for ($i = 1; $i <= $n / 2; $i++)
        if ($marked[$i] == 0)
            array_push($primes, 2 * $i + 1);
}

// modified binary search to find nearest
// prime less than N
function binarySearch($left, $right, $n)
{
    global $primes;
    if ($left <= $right)
    {
        $mid = (int)(($left + $right) / 2);

        // base condition is, if we are reaching
        // at left corner or right corner of
        // primes[] array then return that corner
        // element because before or after that
        // we don't have any prime number in
        // primes array
        if ($mid == 0 || $mid == count($primes) - 1)
            return $primes[$mid];

        // now if n is itself a prime so it will
        // be present in primes array and here
        // we have to find nearest prime less than
        // n so we will return primes[mid-1]
        if ($primes[$mid] == $n)
            return $primes[$mid - 1];

        // now if primes[mid]<n and primes[mid+1]>n
        // that means we reached at nearest prime
        if ($primes[$mid] < $n && $primes[$mid + 1] > $n)
            return $primes[$mid];
        if ($n < $primes[$mid])
            return binarySearch($left, $mid - 1, $n);
        else
            return binarySearch($mid + 1, $right, $n);
    }
    return 0;
}

// Driver Code
Sieve();
$n = 17;
echo binarySearch(0, count($primes) - 1, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

       // JavaScript program to find the nearest prime to n.
       // array to store all primes less than 10^6
       var primes = [];

       // Utility function of Sieve of Sundaram
       var MAX = 1000000;
       function Sieve()
       {
           let n = MAX;

           // In general Sieve of Sundaram, produces primes
           // smaller than (2*x + 2) for a number given
           // number x
           let nNew = parseInt(Math.sqrt(n));

           // This array is used to separate numbers of the
           // form i+j+2ij from others where  1 <= i <= j
           var marked = new Array(n / 2 + 500).fill(0);

           // eliminate indexes which does not produce primes
           for (let i = 1; i <= parseInt((nNew - 1) / 2); i++)
               for (let j = (i * (i + 1)) << 1; j <= parseInt(n / 2); j = j + 2 * i + 1)
                   marked[j] = 1;

           // Since 2 is a prime number
           primes.push(2);

           // Remaining primes are of the form 2*i + 1 such
           // that marked[i] is false.
           for (let i = 1; i <= parseInt(n / 2); i++)
               if (marked[i] == 0)
                   primes.push(2 * i + 1);
       }

       // modified binary search to find nearest prime less than N
       function binarySearch(left, right, n) {
           if (left <= right) {
               let mid = parseInt((left + right) / 2);

               // base condition is, if we are reaching at left
               // corner or right corner of primes[] array then
               // return that corner element because before or
               // after that we don't have any prime number in
               // primes array
               if (mid == 0 || mid == primes.length - 1)
                   return primes[mid];

               // now if n is itself a prime so it will be present
               // in primes array and here we have to find nearest
               // prime less than n so we will return primes[mid-1]
               if (primes[mid] == n)
                   return primes[mid - 1];

               // now if primes[mid]<n and primes[mid+1]>n that
               // mean we reached at nearest prime
               if (primes[mid] < n && primes[mid + 1] > n)
                   return primes[mid];
               if (n < primes[mid])
                   return binarySearch(left, mid - 1, n);
               else
                   return binarySearch(mid + 1, right, n);
           }
           return 0;
       }

       // Driver program to run the case
       Sieve();
       let n = 17;
       document.write(binarySearch(0, primes.length - 1, n));

       // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
13
```

如果你有另一种方法来解决这个问题，那么请在评论中分享。
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。