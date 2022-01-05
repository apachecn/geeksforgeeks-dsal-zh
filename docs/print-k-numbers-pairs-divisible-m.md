# 打印 k 个数字，其中所有对都可以被 m 整除

> 原文:[https://www . geesforgeks . org/print-k-numbers-pairs-除尽-m/](https://www.geeksforgeeks.org/print-k-numbers-pairs-divisible-m/)

给定一个整数数组和两个数字 k 和 m。从数组中打印 k 个数字，这样任意两对之间的差可以被 m 整除。如果没有 k 个数字，则打印-1。
**例:**

```
Input: arr[] = {1, 8, 4}
           k = 2 
           m = 3    
Output: 1 4 
Explanation: Difference between
1 and 4 is divisible by 3.

Input: arr[] = {1, 8, 4} 
       k = 3 
       m = 3 
Output: -1 
Explanation: there are only two numbers 
whose difference is divisible by m, but 
k is three here which is not possible, 
hence we print -1.
```

一种**天真的方法**是对每个元素进行迭代，并与所有其他元素进行检查，如果差可被 m 整除的数字的计数大于或等于 k，那么我们通过再次迭代来打印那些 k 个数字。但是这不够高效，因为它运行两个嵌套循环。
时间复杂度:O(n * n)
辅助空间:O(1)
一种**高效的方法**是应用一种数学方法，在这里我们知道(x-y) % m 是否等于 x % m–y % m。所以如果我们可以存储所有在除以 m 时留下相同余数的数，
并且如果留下相同余数的数的计数大于 k 或者等于 k，那么我们就有了我们的答案，就像所有留下相同余数的数一样。
以下是上述方法的实施

## C++

```
// CPP program to find a list of k elements from
// an array such that difference between all of
// them is divisible by m.
#include <bits/stdc++.h>
using namespace std;

// function to generate k numbers whose difference
// is divisible by m
void print_result(int a[], int n, int k, int m)
{
    // Using an adjacency list like representation
    // to store numbers that lead to same
    // remainder.
    vector<int> v[m];

    for (int i = 0; i < n; i++) {

        // stores the modulus when divided
        // by m
        int rem = a[i] % m;

        v[rem].push_back(a[i]);

        // If we found k elements which
        // have same remainder.
        if (v[rem].size() == k)
        {
            for (int j = 0; j < k; j++)
                cout << v[rem][j] << " ";
            return;            
        }
    }

    // If we could not find k elements
    cout << "-1";
}

// driver program to test the above function
int main()
{
    int a[] = { 1, 8, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    print_result(a, n, 2, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a list of k elements from
// an array such that difference between all of
// them is divisible by m.
import java.util.*;
class GFG
{

// function to generate k numbers whose difference
// is divisible by m
static void print_result(int a[], int n,
                         int k, int m)
{
    // Using an adjacency list like representation
    // to store numbers that lead to same
    // remainder.
    Vector<Vector<Integer>> v = new Vector<Vector<Integer>>(m);
    for(int i = 0; i < m; i++)
        v.add(new Vector<Integer>());

    for (int i = 0; i < n; i++)
    {

        // stores the modulus when divided
        // by m
        int rem = a[i] % m;

        v.get(rem).add(a[i]);

        // If we found k elements which
        // have same remainder.
        if (v.get(rem).size() == k)
        {
            for (int j = 0; j < k; j++)
                System.out.print(v.get(rem).get(j) + " ");
            return;            
        }
    }

    // If we could not find k elements
    System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 8, 4 };
    int n = a.length;
    print_result(a, n, 2, 3);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find a list of k elements from
# an array such that difference between all of
# them is divisible by m.

# function to generate k numbers whose difference
# is divisible by m
def print_result(a, n, k, m):

    # Using an adjacency list like representation
    # to store numbers that lead to same
    # remainder.
    v = [[] for i in range(m)]

    for i in range(0, n):

        # stores the modulus when divided
        # by m
        rem = a[i] % m

        v[rem].append(a[i])

        # If we found k elements which
        # have same remainder.
        if(len(v[rem]) == k):

            for j in range(0, k):
                print(v[rem][j], end=" ")
            return

    # If we could not find k elements
    print(-1)

# driver program to test the above function
if __name__=='__main__':
    a = [1, 8, 4]
    n = len(a)
    print_result(a, n, 2, 3)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find a list of k elements from
// an array such that difference between all of
// them is divisible by m.
using System;
using System.Collections.Generic;

class GFG
{

// function to generate k numbers whose difference
// is divisible by m
static void print_result(int []a, int n,
                         int k, int m)
{
    // Using an adjacency list like representation
    // to store numbers that lead to same
    // remainder.
    List<List<int>> v = new List<List<int>>(m);
    for(int i = 0; i < m; i++)
        v.Add(new List<int>());

    for (int i = 0; i < n; i++)
    {

        // stores the modulus when divided
        // by m
        int rem = a[i] % m;

        v[rem].Add(a[i]);

        // If we found k elements which
        // have same remainder.
        if (v[rem].Count == k)
        {
            for (int j = 0; j < k; j++)
                Console.Write(v[rem][j] + " ");
            return;            
        }
    }

    // If we could not find k elements
    Console.Write("-1");
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 8, 4 };
    int n = a.Length;
    print_result(a, n, 2, 3);
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a list of k elements
// from an array such that difference between
// all of them is divisible by m.

// function to generate k numbers whose
// difference is divisible by m
function print_result($a, $n, $k, $m)
{
    // Using an adjacency list like representation
    // to store numbers that lead to same
    // remainder.
    $v = array_fill(0, $m + 1, array());

    for ($i = 0; $i < $n; $i++)
    {

        // stores the modulus when divided
        // by m
        $rem = $a[$i] % $m;

        array_push($v[$rem], $a[$i]);

        // If we found k elements which
        // have same remainder.
        if (count($v[$rem]) == $k)
        {
            for ($j = 0; $j < $k; $j++)
                echo $v[$rem][$j] . " ";
            return;        
        }
    }

    // If we could not find k elements
    echo "-1";
}

// Driver Code
$a = array( 1, 8, 4 );
$n = count($a);
print_result($a, $n, 2, 3);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find a list of k elements from
// an array such that difference between all of
// them is divisible by m.

// function to generate k numbers whose difference
// is divisible by m
function print_result(a, n, k, m)
{
    // Using an adjacency list like representation
    // to store numbers that lead to same
    // remainder.
    var v = Array.from(Array(m), ()=> Array());

    for (var i = 0; i < n; i++) {

        // stores the modulus when divided
        // by m
        var rem = a[i] % m;

        v[rem].push(a[i]);

        // If we found k elements which
        // have same remainder.
        if (v[rem].length == k)
        {
            for (var j = 0; j < k; j++)
                document.write( v[rem][j] + " ");
            return;            
        }
    }

    // If we could not find k elements
    document.write( "-1");
}

// driver program to test the above function
var a = [1, 8, 4];
var n = a.length;
print_result(a, n, 2, 3);

</script>
```

**输出:**

```
1 4 
```

**时间复杂度:**O(n)
T3】辅助空间: O(m)
本文由[**Raja vikramatitya**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。