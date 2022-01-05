# 每对之和为素数的最大子集

> 原文:[https://www . geesforgeks . org/每对之和最大子集作为质数/](https://www.geeksforgeeks.org/largest-subset-with-sum-of-every-pair-as-prime/)

给定一个数组 A[]，找到最大大小的子集，其中每对元素的和是素数。打印其长度和子集。考虑对不同数组的许多查询，元素的最大值为 100000。
**例:**

```
Input : A[] = {2, 1, 2}
Output : 2
         1 2
Explanation :
Here, we can only form subsets with size 1 and 2.
maximum sized subset = {1, 2}, 1 + 2 = 3, which 
is prime number.
So, Answer = 2 (size), {1, 2} (subset)

Input : A[] = {2, 1, 1}
Output : 3
         1 1 2
Explanation :
Maximum subset = {2, 1, 2}, since 1 + 2 = 3,
1 + 1 = 2, both are prime numbers.
Answer = 3 (size), {2, 1, 1} (subset).
```

让我们做一些观察，然后进入问题。两个数之和是偶数，当且仅当两个数都是奇数或偶数时。除了 2，偶数不能是质数。现在，如果我们取三个数字 a，b 和 c，其中两个应该是奇数或偶数(鸽子洞定理)。因此，我们的解决方案只存在于两种情况下–(让子集为 B)

*   **情况一**:当 B 只包含两个和为素数的整数(> 1)时。
*   **情况二**:当 B 包含若干个 1 和另一个数 X，其中 X + 1 应该是素数(只有当 X 是偶数时才有可能)。

首先使用 for 循环计算数组中 1 的个数。

1.  如果 1 的计数大于 0，则遍历整个数组并检查[A[i] + 1]是否是素数和(A[i]！= 1)，如果找到，打印子阵列的大小为*(1 的计数)* +1 和所有的 1 以及找到的 A[i]。退出程序。
2.  如果上述步骤失败(即未找到 A[i])，打印所有 1。退出程序。
3.  如果上述步骤失败(即*计数为 1s = 0* ，检查数组中的每对元素的和是否为素数。打印 2 和整数对。
4.  否则打印-1。

以下是上述方法的实施:

## C++

```
// CPP program to find a subset in which sum of
// every pair in it is a prime
#include <bits/stdc++.h>
using namespace std;

#define MAX 100001

bool isPrime[MAX] = { 0 };

int sieve()
{
    for (int p = 2; p * p < MAX; p++)
    {
        // If isPrime[p] is not changed, then it
        // is a prime
        if (isPrime[p] == 0)
        {
            // Update all multiples of p
            for (int i = p * 2; i < MAX; i += p)
                isPrime[i] = 1;
        }
    }
}

int findSubset(int a[], int n)
{
    int cnt1 = 0;

    // Counting no.of ones in the array
    for (int i = 0; i < n; i++)
        if (a[i] == 1)
            cnt1++;

    // Case-I: count of ones(1s) > 0 and
    // an integer > 1 is present in the array
    if (cnt1 > 0)
    {
        for (int i = 0; i < n; i++)
        {
            // Find a[i], where a[i] + 1 is prime.
            if ((a[i] != 1) and (isPrime[a[i] + 1] == 0))
            {
                cout << cnt1 + 1 << endl;

                // Print all the ones(1s).
                for (int j = 0; j < cnt1; j++)

                cout << 1 << " ";
                cout << a[i] << endl; // print a[i].
                return 0;
            }
        }
    }

    // Case-II: array contains only ones(1s)
    if (cnt1 >= 2)
    {
        cout << cnt1 << endl;

        // Print all ones(1s).
        for (int i = 0; i < cnt1; i++)
            cout << 1 << " ";

        cout << endl;
        return 0;
    }

    // Case-III: array does not contain 1s
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            // Find a pair of integers whose sum is prime
            if (isPrime[a[i] + a[j]] == 0)
            {
                cout << 2 << endl;
                cout << a[i] << " " << a[j] << endl;
                return 0;
            }
        }
    }

    // Array contains only a single element.
    cout << -1 << endl;
}

// Driver function
int main()
{
    sieve();
    int A[] = { 2, 1, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    findSubset(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a
// subset in which sum of
// every pair in it is a prime
import java.io.*;

class GFG
{
    static int MAX = 100001;

    static int []isPrime = new int[MAX];

    static int sieve()
    {
        for (int p = 2;
                 p * p < MAX; p++)
        {
            // If isPrime[p] is
            // not changed, then
            // it is a prime
            if (isPrime[p] == 0)
            {
                // Update all
                // multiples of p
                for (int i = p * 2;
                         i < MAX; i += p)
                    isPrime[i] = 1;
            }
        }
        return -1;
    }    
    static int findSubset(int []a, int n)
    {
        int cnt1 = 0;

        // Counting no. of
        // ones in the array
        for (int i = 0; i < n; i++)
            if (a[i] == 1)
                cnt1++;

        // Case-I: count of
        // ones(1s) > 0 and
        // an integer > 1 is
        // present in the array
        if (cnt1 > 0)
        {
            for (int i = 0; i < n; i++)
            {
                // Find a[i], where
                // a[i] + 1 is prime.
                if ((a[i] != 1) &&
                    (isPrime[a[i] + 1] == 0))
                {
                    System.out.println(cnt1 + 1);

                    // Print all
                    // the ones(1s).
                    for (int j = 0;
                             j < cnt1; j++)

                    System.out.print(1 + " ");
                    System.out.println(a[i]); // print a[i].
                    return 0;
                }
            }
        }

        // Case-II: array contains
        // only ones(1s)
        if (cnt1 >= 2)
        {
            System.out.println(cnt1);

            // Print all ones(1s).
            for (int i = 0;
                     i < cnt1; i++)
                System.out.print(1 + " ");

            System.out.println();
            return 0;
        }

        // Case-III: array does
        // not contain 1s
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1;
                     j < n; j++)
            {
                // Find a pair of integers
                // whose sum is prime
                if (isPrime[a[i] + a[j]] == 0)
                {
                    System.out.println(2);
                    System.out.println(a[i] +
                                 " " + a[j]);
                    return 0;
                }
            }
        }

        // Array contains only
        // a single element.
        System.out.println(-1);
        return -1;
    }

    // Driver Code
    public static void main(String args[])
    {
        sieve();
        int []A = new int[]{ 2, 1, 1 };
        int n = A.length;
        findSubset(A, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find a subset in which
# sum of every pair in it is a prime
import math as mt

MAX = 100001

isPrime = [0 for i in range(MAX)]

def sieve():

    for p in range(2, mt.ceil(mt.sqrt(MAX))):

        # If isPrime[p] is not changed,
        # then it is a prime
        if (isPrime[p] == 0) :

            # Update all multiples of p
            for i in range(2 * p, MAX, p):
                isPrime[i] = 1

def findSubset(a, n):

    cnt1 = 0

    # Counting no.of ones in the array
    for i in range(n):
        if (a[i] == 1):
            cnt1+=1

    # Case-I: count of ones(1s) > 0 and
    # an integer > 1 is present in the array
    if (cnt1 > 0):

        for i in range(n):

            # Find a[i], where a[i] + 1 is prime.
            if ((a[i] != 1) and
                (isPrime[a[i] + 1] == 0)):

                print(cnt1 + 1)

                # Print all the ones(1s).
                for j in range(cnt1):
                    print("1", end = " ")

                print(a[i])
                return 0

    # Case-II: array contains only ones(1s)
    if (cnt1 >= 2):

        print(cnt1)

        # Print all ones(1s).
        for i in range(cnt1):
            print("1", end = " ")

        print("\n")
        return 0

    # Case-III: array does not contain 1s
    for i in range(n):
        for j in range(i + 1, n):

            # Find a pair of integers whose
            # sum is prime
            if (isPrime[a[i] + a[j]] == 0):
                print(2)
                print(a[i], " ", a[j])

    # Array contains only a single element.
    print(-1)

# Driver Code
sieve()
A =[ 2, 1, 1]
n =len(A)
findSubset(A, n)

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to find a subset
// in which sum of every pair
// in it is a prime
using System;

class GFG
{
    static int MAX = 100001;

    static int []isPrime = new int[MAX];

    static int sieve()
    {
        for (int p = 2;
                 p * p < MAX; p++)
        {
            // If isPrime[p] is
            // not changed, then
            // it is a prime
            if (isPrime[p] == 0)
            {
                // Update all
                // multiples of p
                for (int i = p * 2;
                         i < MAX; i += p)
                    isPrime[i] = 1;
            }
        }
        return -1;
    }    
    static int findSubset(int []a, int n)
    {
        int cnt1 = 0;

        // Counting no. of
        // ones in the array
        for (int i = 0; i < n; i++)
            if (a[i] == 1)
                cnt1++;

        // Case-I: count of
        // ones(1s) > 0 and
        // an integer > 1 is
        // present in the array
        if (cnt1 > 0)
        {
            for (int i = 0; i < n; i++)
            {
                // Find a[i], where
                // a[i] + 1 is prime.
                if ((a[i] != 1) &&
                    (isPrime[a[i] + 1] == 0))
                {
                    Console.WriteLine(cnt1 + 1);

                    // Print all the ones(1s).
                    for (int j = 0; j < cnt1; j++)

                    Console.Write(1 + " ");
                    Console.WriteLine(a[i]); // print a[i].
                    return 0;
                }
            }
        }

        // Case-II: array contains
        // only ones(1s)
        if (cnt1 >= 2)
        {
            Console.WriteLine(cnt1);

            // Print all ones(1s).
            for (int i = 0; i < cnt1; i++)
                Console.Write(1 + " ");

            Console.WriteLine();
            return 0;
        }

        // Case-III: array does
        // not contain 1s
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                // Find a pair of integers
                // whose sum is prime
                if (isPrime[a[i] + a[j]] == 0)
                {
                    Console.WriteLine(2);
                    Console.WriteLine(a[i] + " " + a[j]);
                    return 0;
                }
            }
        }

        // Array contains only
        // a single element.
        Console.WriteLine(-1);
        return -1;
    }

    // Driver Code
    static void Main()
    {
        sieve();
        int []A = new int[]{ 2, 1, 1 };
        int n = A.Length;
        findSubset(A, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// a subset in which
// sum of every pair in
// it is a prime
$MAX = 100001;

$isPrime = array();
for($i = 0;
    $i < $MAX; $i++)
    $isPrime[$i] = 0;

function sieve()
{
    global $MAX, $isPrime;
    for ($p = 2;
         $p * $p < $MAX; $p++)
    {
        // If isPrime[p] is not
        // changed, then it is
        // a prime
        if ($isPrime[$p] == 0)
        {
            // Update all
            // multiples of p
            for ($i = $p * 2;
                 $i < $MAX; $i += $p)
                $isPrime[$i] = 1;
        }
    }
}

function findSubset($a, $n)
{
    $cnt1 = 0;
    global $MAX, $isPrime;

    // Counting no.of
    // ones in the array
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] == 1)
            $cnt1++;

    // Case-I: count of
    // ones(1s) > 0 and
    // an integer > 1 is
    // present in the array
    if ($cnt1 > 0)
    {
        for ($i = 0; $i < $n; $i++)
        {
            // Find a[i], where
            // a[i] + 1 is prime.
            if (($a[$i] != 1) and
                ($isPrime[$a[$i] + 1] == 0))
            {
                echo (($cnt1 + 1) . "\n");

                // Pr$all the ones(1s).
                for ($j = 0;
                     $j < $cnt1; $j++)
                {
                    echo ("1 ");
                }
                echo ($a[$i] . "\n");
                return 0;
            }
        }
    }

    // Case-II: array contains
    // only ones(1s)
    if ($cnt1 >= 2)
    {
        echo (cnt1 . "\n");

        // Pr$all ones(1s).
        for ($i = 0;
             $i < $cnt1; $i++)
            echo ("1 ");

        echo ("\n");
        return 0;
    }

    // Case-III: array does
    // not contain 1s
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1;
             $j < $n; $j++)
        {
            // Find a pair of integers
            // whose sum is prime
            if ($isPrime[$a[$i] +
                $a[$j]] == 0)
            {
                echo (2 . "\n");
                echo ($a[$i] . " " .
                      $a[$j] . "\n");
                return 0;
            }
        }
    }

    // Array contains only
    // a single element.
    echo (-1 . "\n");
}

// Driver Code
sieve();
$A = array(2, 1, 1);
$n = count($A);
findSubset($A, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to find a
// subset in which sum of
// every pair in it is a prime

    let MAX = 100001;
    let isPrime = new Array(MAX);
    for(let i=0;i<MAX;i++)
    {
        isPrime[i]=0;
    }

    function sieve()
    {
        for (let p = 2;
                 p * p < MAX; p++)
        {
            // If isPrime[p] is
            // not changed, then
            // it is a prime
            if (isPrime[p] == 0)
            {
                // Update all
                // multiples of p
                for (let i = p * 2;
                         i < MAX; i += p)
                    isPrime[i] = 1;
            }
        }
        return -1;
    }

    function findSubset(a,n)
    {
        let cnt1 = 0;

        // Counting no. of
        // ones in the array
        for (let i = 0; i < n; i++)
            if (a[i] == 1)
                cnt1++;

        // Case-I: count of
        // ones(1s) > 0 and
        // an integer > 1 is
        // present in the array
        if (cnt1 > 0)
        {
            for (let i = 0; i < n; i++)
            {
                // Find a[i], where
                // a[i] + 1 is prime.
                if ((a[i] != 1) &&
                    (isPrime[a[i] + 1] == 0))
                {
                    document.write((cnt1 + 1)+"<br>");

                    // Print all
                    // the ones(1s).
                    for (let j = 0;
                             j < cnt1; j++)

                    document.write(1 + " ");
                    // print a[i].
                    document.write(a[i]+"<br>");
                    return 0;
                }
            }
        }

        // Case-II: array contains
        // only ones(1s)
        if (cnt1 >= 2)
        {
            document.write(cnt1);

            // Print all ones(1s).
            for (let i = 0;
                     i < cnt1; i++)
                document.write(1 + " ");

            document.write("<br>");
            return 0;
        }

        // Case-III: array does
        // not contain 1s
        for (let i = 0; i < n; i++)
        {
            for (let j = i + 1;
                     j < n; j++)
            {
                // Find a pair of integers
                // whose sum is prime
                if (isPrime[a[i] + a[j]] == 0)
                {
                    document.write(2+"<br>");
                    document.write(a[i] +
                                 " " + a[j]+"<br>");
                    return 0;
                }
            }
        }

        // Array contains only
        // a single element.
        document.write(-1);
        return -1;
    }

    // Driver Code
    sieve();
    let A=[2, 1, 1 ];
    let n = A.length;
    findSubset(A, n);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
3
1 1 2
```

**时间复杂度:** O(n <sup>2</sup> )