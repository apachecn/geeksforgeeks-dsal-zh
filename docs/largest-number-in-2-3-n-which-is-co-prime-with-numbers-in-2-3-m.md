# 在[2，3，..n]与[2，3，..m]

> 原文:[https://www . geesforgeks . org/2-3-n 中的最大数字与 2-3-m 中的数字同素/](https://www.geeksforgeeks.org/largest-number-in-2-3-n-which-is-co-prime-with-numbers-in-2-3-m/)

给定两个整数 n 和 m，任务是找到一个满足以下条件的数 p:
->数 p 应小于或等于 n。
->数应与从 2 到 p(含)的所有整数同素，即两个数除的唯一正整数为 1。
**例:**

```
Input :  n = 16, m = 3
Output : 13
Explanation : We need to find largest number
smaller than n and co-prime with all numbers
in set [2, 3, ... m] which is [2, 3] here. 
Note that numbers {2, 4, 6, 8, ..} are not
co-prime with 2 and numbers {3, 6, 9, .. }
are not co-prime with 3.

Input : n = 6, m = 5
Output : -1 (Number doesn't exists)
Explanation : In this example 2 will cancel
out 2, 4, 6 and 3 will cancel out 3, 6
and 5 will cancel out 5\. No number is left, 
so the answer does not exists.
```

**方法 1 :** 创建一个从 2 到 n 的数字列表，然后运行 i = 2 到 m 的循环，标记所有 I 的倍数的数字，如果 I 已经被标记，不要运行循环，因为它的倍数已经被标记了。当循环终止时，运行一个从 n 到 2 的循环，直到找到一个未标记的数字。第一个未标记的数字就是答案，如果没有未标记的数字，那么这个数字就不存在。这种方法需要 O(n)个辅助空间，因此如果 n 的值太大，这种方法将不起作用。
**方法 2 :** 运行一个从 n 到 p+1 的循环，检查每个数是否不能被 2 到 m 之间的任何数整除。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Returns true if i is co-prime with numbers
// in set [2, 3, ... m]
bool isValid(long long int i, long long int m)
{
    // Running the loop till square root of n
    // to reduce the time complexity from n
    long long int sq_i = sqrt(i);

    // Find the minimum of square root of n
    // and m to run the loop until the smaller
    // one
    long long int sq = min(m, sq_i);

    // Check from 2 to min(m, sqrt(n))
    for (long long int j = 2; j <= sq; j++)
        if (i % j == 0)
            return false;

    return true;
}

// Function to find the largest number less than n
// which is Co-prime with all numbers from 2 to m
void findLargestNum(long long int n, long long int m)
{
    // Iterating from n to m+1 to find the number
    for (long long int i = n; i > m; i--) {

        // checking every number for the given
        // conditions
        if (isValid(i, m)) {

            // The first number which satisfy the
            // conditions is the answer
            cout << i << '\n';
            return;
        }
    }

    // If there is no number which satisfy the
    // conditions, then print number does not exist.
    cout << "Number Doesn't Exists\n";
}

// Driver Program
int main()
{
    long long int n = 16, m = 3;
    findLargestNum(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Largest number in [2, 3, .. n]
// which is co-prime with numbers
// in [2, 3, .. m]
import java.io.*;

class GFG
{
    // Returns true if i is co-prime with numbers
    // in set [2, 3, ... m]
    static boolean isValid(long i, long m)
    {
        // Running the loop till square root of n
        // to reduce the time complexity from n
        long sq_i = (long)Math.sqrt(i);

        // Find the minimum of square root of n
        // and m to run the loop until the smaller
        // one
        long sq = Math.min(m, sq_i);

        // Check from 2 to min(m, sqrt(n))
        for (long j = 2; j <= sq; j++)
            if (i % j == 0)
                return false;

        return true;
    }

    // Function to find the largest number less than n
    // which is Co-prime with all numbers from 2 to m
    static void findLargestNum(long n, long m)
    {
        // Iterating from n to m+1 to find the number
        for (long i = n; i > m; i--) {

            // checking every number for the given
            // conditions
            if (isValid(i, m)) {

                // The first number which satisfy the
                // conditions is the answer
                System.out.println (i);
                return;
            }
        }

        // If there is no number which satisfy the
        // conditions, then print number does not exist.
        System.out.println("Number Doesn't Exists");
    }

    // Driver Program
    public static void main (String[] args)
    {
        long n = 16, m = 3;
        findLargestNum(n, m);

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find
# Largest number in
# [2, 3, .. n] which is
# co-prime with
# numbers in [2, 3, .. m]
import math

# Returns true if i is
# co-prime with numbers
# in set [2, 3, ... m]
def isValid(i,m) :

    # Running the loop
    # till square root of n
    # to reduce the time
    # complexity from n
    sq_i = math.sqrt(i)

    # Find the minimum of
    # square root of n
    # and m to run the loop
    # until the smaller
    # one
    sq = min(m, sq_i)

    # Check from 2 to
    # min(m, sqrt(n))
    for j in range(2, sq + 1) :
        if (i % j == 0) :
            return False

    return True

# def to find the
# largest number less
# than n which is Co-prime 
# with all numbers from
# 2 to m
def findLargestNum(n, m) :

    # Iterating from n to m+1
    # to find the number
    for i in range(n, m, -1) :

        # checking every number for
        # the given conditions
        if (isValid(i, m)) :

            # The first number
            # which satisfy the
            # conditions is the
            # answer
            print ("{}\n".format(i));
            return

    # If there is no number
    # which satisfy the
    # conditions, then print
    # number does not exist.
    print ("Number Doesn't Exists\n")

# Driver Code
n = 16
m = 3
findLargestNum(n, m)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Largest number in [2, 3, .. n]
// which is co-prime with numbers
// in [2, 3, .. m]
using System;

class GFG
{
    // Returns true if i is co-prime
    // with numbers in set [2, 3, ... m]
    static bool isValid(long i, long m)
    {
        // Running the loop till square root
        // of n to reduce the time complexity
        // from n
        long sq_i = (long)Math.Sqrt(i);

        // Find the minimum of square root
        // of n and m to run the loop until
        // the smaller one
        long sq = Math.Min(m, sq_i);

        // Check from 2 to min(m, sqrt(n))
        for (long j = 2; j <= sq; j++)
            if (i % j == 0)
                return false;

        return true;
    }

    // Function to find the largest number
    // less than n which is Co-prime with
    // all numbers from 2 to m
    static void findLargestNum(long n, long m)
    {
        // Iterating from n to m+1 to find the
        // number
        for (long i = n; i > m; i--) {

            // checking every number for the given
            // conditions
            if (isValid(i, m)) {

                // The first number which satisfy the
                // conditions is the answer
                Console.WriteLine(i);
                return;
            }
        }

        // If there is no number which satisfy
        // the conditions, then print number does
        // not exist.
        Console.WriteLine("Number Doesn't Exists");
    }

    // Driver Program
    public static void Main ()
    {
        long n = 55, m = 25;
        findLargestNum(n, m);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find Largest number in 
// [2, 3, .. n] which is co-prime with 
// numbers in [2, 3, .. m]

// Returns true if i is
// co-prime with numbers
// in set [2, 3, ... m]
function isValid($i,$m)
{

    // Running the loop
    // till square root of n
    // to reduce the time
    // complexity from n
    $sq_i = sqrt($i);

    // Find the minimum of
    // square root of n
    // and m to run the loop
    // until the smaller
    // one
    $sq = min($m, $sq_i);

    // Check from 2 to
    // min(m, sqrt(n))
    for ($j = 2; $j <= $sq; $j++)
        if ($i % $j == 0)
            return false;

    return true;
}

// Function to find the
// largest number less than n
// which is Co-prime with
// all numbers from 2 to m
function findLargestNum($n, $m)
{

    // Iterating from n to m+1
    // to find the number
    for ($i = $n; $i > $m; $i--)
    {

        // checking every number for
        // the given conditions
        if (isValid($i, $m))
        {

            // The first number
            // which satisfy the
            // conditions is the
            // answer
            echo $i , "\n";
            return;
        }
    }

    // If there is no number
    // which satisfy the
    // conditions, then print
    // number does not exist.
    echo "Number Doesn't Exists\n";
}

    // Driver Code
    $n = 16; $m = 3;
    findLargestNum($n, $m);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>
// JavaScript program to find Largest number in [2, 3, .. n]
// which is co-prime with numbers
// in [2, 3, .. m]

    // Returns true if i is co-prime with numbers
    // in set [2, 3, ... m]
    function isValid(i, m)
    {
        // Running the loop till square root of n
        // to reduce the time complexity from n
        let sq_i = Math.sqrt(i);

        // Find the minimum of square root of n
        // and m to run the loop until the smaller
        // one
        let sq = Math.min(m, sq_i);

        // Check from 2 to min(m, sqrt(n))
        for (let j = 2; j <= sq; j++)
            if (i % j == 0)
                return false;

        return true;
    }

    // Function to find the largest number less than n
    // which is Co-prime with all numbers from 2 to m
    function findLargestNum(n, m)
    {
        // Iterating from n to m+1 to find the number
        for (let i = n; i > m; i--) {

            // checking every number for the given
            // conditions
            if (isValid(i, m)) {

                // The first number which satisfy the
                // conditions is the answer
                document.write (i);
                return;
            }
        }

        // If there is no number which satisfy the
        // conditions, then print number does not exist.
        document.write("Number Doesn't Exists");
    }

// Driver Code

        let n = 16, m = 3;
        findLargestNum(n, m);

// This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
13
```