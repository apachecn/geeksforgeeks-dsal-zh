# 桥头堡

> 哎哎哎:# t0]https://www . geeksforgeeks . org/pierppont-prime/

A [皮尔庞特素数](http://mathworld.wolfram.com/PierpontPrime.html)是 p = 2<sup>l</sup>3<sup>k</sup>+1 形式的素数。前几个皮尔庞特素数是 2，3，5，7，13，17，19，37，73，97，109，…
给定一个数 **n** ，任务是打印小于 n 的皮尔庞特素数
**示例:**

```
Input : n = 15
Output : 2 3 5 7 13

Input : n = 200
Output : 2 3 5 7 13 17 19 37 
         73 97 109 163 193
```

这个想法是找到只有 2 和 3 的幂的数。现在用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)求所有质数。最后，打印两个序列的公共编号。
以下是本办法的实施情况:

## C++

```
// CPP program to print Pierpont prime
// numbers smaller than n.
#include <bits/stdc++.h>
using namespace std;

bool printPierpont(int n)
{   
    // Finding all numbers having factor power
    // of 2 and 3 Using sieve
    bool arr[n+1];
    memset(arr, false, sizeof arr);
    int two = 1, three = 1;
    while (two + 1 < n) {
        arr[two] = true;
        while (two * three + 1 < n) {
            arr[three] = true;
            arr[two * three] = true;
            three *= 3;
        }
        three = 1;
        two *= 2;
    }

    // Storing number of the form 2^i.3^k + 1.
    vector<int> v;
    for (int i = 0; i < n; i++)
        if (arr[i])
            v.push_back(i + 1);   

    // Finding prime number using sieve of
    // Eratosthenes. Reusing same array as
    // result of above computations in v.
    memset(arr, false, sizeof arr);
    for (int p = 2; p * p < n; p++) {
        if (arr[p] == false)
            for (int i = p * 2; i < n; i += p)
                arr[i] = true;
    }

    // Printing n pierpont primes smaller than n
    for (int i = 0; i < v.size(); i++)
        if (!arr[v[i]])
            cout << v[i] << " ";
}

// Driven Program
int main()
{
    int n = 200;
    printPierpont(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Pierpont prime
// numbers smaller than n.
import java.util.*;
class GFG{
static void printPierpont(int n)
{
    // Finding all numbers having factor power
    // of 2 and 3 Using sieve
    boolean[] arr=new boolean[n+1];
    int two = 1, three = 1;
    while (two + 1 < n) {
        arr[two] = true;
        while (two * three + 1 < n) {
            arr[three] = true;
            arr[two * three] = true;
            three *= 3;
        }
        three = 1;
        two *= 2;
    }

    // Storing number of the form 2^i.3^k + 1.
    ArrayList<Integer> v=new ArrayList<Integer>();
    for (int i = 0; i < n; i++)
        if (arr[i])
            v.add(i + 1);

    // Finding prime number using sieve of
    // Eratosthenes. Reusing same array as
    // result of above computations in v.
    arr=new boolean[n+1];
    for (int p = 2; p * p < n; p++) {
        if (arr[p] == false)
            for (int i = p * 2; i < n; i += p)
                arr[i] = true;
    }

    // Printing n pierpont primes smaller than n
    for (int i = 0; i < v.size(); i++)
        if (!arr[v.get(i)])
            System.out.print(v.get(i)+" ");
}

// Driven Program
public static void main(String[] args)
{
    int n = 200;
    printPierpont(n);
}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print Pierpont
# prime numbers smaller than n.

def printPierpont(n):

    # Finding all numbers having factor
    # power of 2 and 3 Using sieve
    arr = [False] * (n + 1);
    two = 1;
    three = 1;
    while (two + 1 < n):
        arr[two] = True;
        while (two * three + 1 < n):
            arr[three] = True;
            arr[two * three] = True;
            three *= 3;

        three = 1;
        two *= 2;

    # Storing number of the form 2^i.3^k + 1.
    v = [];
    for i in range(n):
        if (arr[i]):
            v.append(i + 1);

    # Finding prime number using
    # sieve of Eratosthenes.
    # Reusing same array as result
    # of above computations in v.
    arr1 = [False] * (len(arr));
    p = 2;
    while (p * p < n):
        if (arr1[p] == False):
            for i in range(p * 2, n, p):
                arr1[i] = True;
        p += 1;

    # Printing n pierpont primes
    # smaller than n
    for i in range(len(v)):
        if (not arr1[v[i]]):
            print(v[i], end = " ");

# Driver Code
n = 200;
printPierpont(n);

# This code is contributed by mits
```

## C#

```
// C# program to print Pierpont prime
// numbers smaller than n.
using System;
using System.Collections;

class GFG{
static void printPierpont(int n)
{
    // Finding all numbers having factor power
    // of 2 and 3 Using sieve
    bool[] arr=new bool[n+1];
    int two = 1, three = 1;
    while (two + 1 < n) {
        arr[two] = true;
        while (two * three + 1 < n) {
            arr[three] = true;
            arr[two * three] = true;
            three *= 3;
        }
        three = 1;
        two *= 2;
    }

    // Storing number of the form 2^i.3^k + 1.
    ArrayList v=new ArrayList();
    for (int i = 0; i < n; i++)
        if (arr[i])
            v.Add(i + 1);

    // Finding prime number using sieve of
    // Eratosthenes. Reusing same array as
    // result of above computations in v.
    arr=new bool[n+1];
    for (int p = 2; p * p < n; p++) {
        if (arr[p] == false)
            for (int i = p * 2; i < n; i += p)
                arr[i] = true;
    }

    // Printing n pierpont primes smaller than n
    for (int i = 0; i < v.Count; i++)
        if (!arr[(int)v[i]])
            Console.Write(v[i]+" ");
}

// Driven Program
static void Main()
{
    int n = 200;
    printPierpont(n);
}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// Pierpont prime numbers
// smaller than n.

function printPierpont($n)
{
    // Finding all numbers
    // having factor power
    // of 2 and 3 Using sieve
    $arr = array_fill(0, $n + 1, false);
    $two = 1;
    $three = 1;
    while ($two + 1 < $n)
    {
        $arr[$two] = true;
        while ($two * $three + 1 < $n)
        {
            $arr[$three] = true;
            $arr[$two * $three] = true;
            $three *= 3;
        }
        $three = 1;
        $two *= 2;
    }

    // Storing number of the
    // form 2^i.3^k + 1.
    $v;
    $x = 0;
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i])
            $v[$x++] = $i + 1;

    // Finding prime number using
    // sieve of Eratosthenes.
    // Reusing same array as result
    // of above computations in v.
    $arr1 = array_fill(0, count($arr), false);
    for ($p = 2;
         $p * $p < $n; $p++)
    {
        if ($arr1[$p] == false)
            for ($i = $p * 2;
                 $i < $n; $i += $p)
                $arr1[$i] = true;
    }

    // Printing n pierpont
    // primes smaller than n
    for ($i = 0; $i < $x; $i++)
        if (!$arr1[$v[$i]])
            echo $v[$i] . " ";
}

// Driver Code
$n = 200;
printPierpont($n);

// This Code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print Pierpont prime
// numbers smaller than n.

function printPierpont(n)
{   
    // Finding all numbers having factor power
    // of 2 and 3 Using sieve
    var arr = Array(n+1).fill(false);
    var two = 1, three = 1;
    while (two + 1 < n) {
        arr[two] = true;
        while (two * three + 1 < n) {
            arr[three] = true;
            arr[two * three] = true;
            three *= 3;
        }
        three = 1;
        two *= 2;
    }

    // Storing number of the form 2^i.3^k + 1.
    var v = [];
    for (var i = 0; i < n; i++)
        if (arr[i])
            v.push(i + 1);   

    // Finding prime number using sieve of
    // Eratosthenes. Reusing same array as
    // result of above computations in v.
    arr = Array(n+1).fill(false);

    for (var p = 2; p * p < n; p++) {
        if (arr[p] == false)
            for (var i = p * 2; i < n; i += p)
                arr[i] = true;
    }

    // Printing n pierpont primes smaller than n
    for (var i = 0; i < v.length; i++)
        if (!arr[v[i]])
            document.write( v[i] + " ");
}

// Driven Program
var n = 200;
printPierpont(n);

</script>
```

**输出:**

```
2 3 5 7 13 17 19 37 73 97 109 163 193
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。