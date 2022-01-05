# 检查任何子集的按位“与”是否为 2 的幂

> 原文:[https://www . geesforgeks . org/check-bitwise-subset-power-two/](https://www.geeksforgeeks.org/check-bitwise-subset-power-two/)

给定正整数的数组**arr[]****n**。任务是检查数组中是否存在按位“与”是 2 的幂的子集(即 1，2，4，8，16，…)。
示例:

```
Input : n = 3, arr[] = { 12, 13, 7 }
Output : Yes
Subset { 12, 7 } has Bitwise AND value 4, which 
is power of 2.

Input : n = 2, arr[] = { 10, 20 }
Output : No
```

注意，对于 2 的幂的数字，它应该只有 1 个设置位。
如果 n 为 1，那么我们只需检查该数字是否只有一个设置位。
对于大于 1 的 n，我们的任务变成从数组中选择那些数字，这些数字的按位“与”导致一个唯一的单比特组数。为此，我们搜索一个位置，集合中的所有元素在该位置都有一个位集。例如，对于集合{ 4 (100)、6 (110)、7 (111) }，在位置 2(从右到左，基于 0 的索引)为所有元素设置了位。所以，按位“与”得到 4，是 2 的幂。
以下是本办法的实施情况:

## C++

```
// CPP Program to check if Bitwise AND of any
// subset is power of two
#include <bits/stdc++.h>
using namespace std;

const int NUM_BITS = 32;

// Check for power of 2 or not
bool isPowerOf2(int num)
{
    return (num && !(num & (num - 1)));
}

// Check if there exist a subset whose bitwise AND
// is power of 2.
bool checkSubsequence(int arr[], int n)
{
    // if there is only one element in the set.
    if (n == 1)
       return isPowerOf2(arr[0]);

    // Finding a number with all bit sets.
    int total = 0;
    for (int i = 0; i < NUM_BITS; i++)
        total = total | (1 << i);

    // check all the positions at which the bit is set.
    for (int i = 0; i < NUM_BITS; i++) {

        int ans = total;
        for (int j = 0; j < n; j++) {

            // include all those elements whose
            // i-th bit is set
            if (arr[j] & (1 << i))
                ans = ans & arr[j];
        }

        // check for the set contains elements
        // make a power of 2 or not
        if (isPowerOf2(ans))
            return true;
    }
    return false;
}

// Driver Program
int main()
{
    int arr[] = { 12, 13, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (checkSubsequence(arr, n))
        printf("YES\n");
    else
        printf("NO\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if Bitwise AND of any
// subset is power of two
import java.io.*;
import java.util.*;

public class GFG {

    static int NUM_BITS = 32;

    // Check for power of 2 or not
    static boolean isPowerOf2(int num)
    {
        if(num != 0 && (num & (num - 1)) == 0)
            return true;
        return false;
    }

    // Check if there exist a
    // subset whose bitwise AND
    // is power of 2.
    static boolean checkSubsequence(int []arr, int n)
    {

        // if there is only one
        // element in the set.
        if (n == 1)
            return isPowerOf2(arr[0]);

        // Finding a number with
        // all bit sets.
        int total = 0;
        for (int i = 0; i < NUM_BITS; i++)
            total = total | (1 << i);

        // check all the positions
        // at which the bit is set.
        for (int i = 0; i < NUM_BITS; i++)
        {

            int ans = total;
            for (int j = 0; j < n; j++)
            {

                // include all those
                // elements whose
                // i-th bit is set
                int p = arr[j] & (1 << i);
                if (p == 0)
                    ans = ans & arr[j];
            }

            // check for the set
            // contains elements
            // make a power of 2
            // or not
            if (isPowerOf2(ans))
                return true;
        }
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        int []arr = {12, 13, 7};
        int n = arr.length;
        if (checkSubsequence(arr, n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python3 Program to check if Bitwise AND of any
# subset is power of two

NUM_BITS = 32

# Check for power of 2 or not
def isPowerOf2(num):
    return (num and (num & (num - 1)) == 0)

# Check if there exist a subset whose bitwise AND
# is power of 2.
def checkSubsequence(arr, n):

    # if there is only one element in the set.
    if (n == 1):
        return isPowerOf2(arr[0])

    # Finding a number with all bit sets.
    total = 0
    for i in range(0, NUM_BITS):
        total = total | (1 << i)

    # check all the positions at which the bit is set.
    for i in range(0, NUM_BITS):

        ans = total
        for j in range(0, n):

            # include all those elements whose
            # i-th bit is set
            if (arr[j] & (1 << i)):
                ans = ans & arr[j]

        # check for the set contains elements
        # make a power of 2 or not
        if (isPowerOf2(ans)):
            return True
    return False

# Driver Program
arr = [ 12, 13, 7 ]
n = len(arr)
if (checkSubsequence(arr, n)):
    print ("YES\n")
else:
    print ("NO\n")

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# Program to check if Bitwise AND of any
// subset is power of two
using System;
using System.Collections.Generic;

class GFG {

    static int NUM_BITS = 32;

    // Check for power of 2 or not
    static bool isPowerOf2(int num)
    {
        if(num != 0 && (num & (num - 1)) == 0)
            return true;
        return false;
    }

    // Check if there exist a
    // subset whose bitwise AND
    // is power of 2.
    static bool checkSubsequence(int []arr, int n)
    {

        // if there is only one
        // element in the set.
        if (n == 1)
            return isPowerOf2(arr[0]);

        // Finding a number with
        // all bit sets.
        int total = 0;
        for (int i = 0; i < NUM_BITS; i++)
            total = total | (1 << i);

        // check all the positions
        // at which the bit is set.
        for (int i = 0; i < NUM_BITS; i++)
        {

            int ans = total;
            for (int j = 0; j < n; j++)
            {

                // include all those
                // elements whose
                // i-th bit is set
                int p = arr[j] & (1 << i);
                if (p == 0)
                    ans = ans & arr[j];
            }

            // check for the set
            // contains elements
            // make a power of 2
            // or not
            if (isPowerOf2(ans))
                return true;
        }
        return false;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {12, 13, 7};
        int n = arr.Length;
        if (checkSubsequence(arr, n))
            Console.Write("YES\n");
        else
            Console.Write("NO\n");
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if
// Bitwise AND of any subset
// is power of two

// Check for power of 2 or not
function isPowerOf2($num)
{
    return ($num && !($num & ($num - 1)));
}

// Check if there exist a
// subset whose bitwise AND
// is power of 2.
function checkSubsequence($arr, $n)
{
    $NUM_BITS = 32;

    // if there is only one
    // element in the set.
    if ($n == 1)
    return isPowerOf2($arr[0]);

    // Finding a number with
    // all bit sets.
    $total = 0;
    for($i = 0; $i < $NUM_BITS; $i++)
        $total = $total | (1 << $i);

    // check all the positions at
    // which the bit is set.
    for($i = 0; $i < $NUM_BITS; $i++)
    {

        $ans = $total;
        for ($j = 0; $j < $n; $j++)
        {

            // include all those
            // elements whose
            // i-th bit is set
            if ($arr[$j] & (1 << $i))
                $ans = $ans & $arr[$j];
        }

        // check for the set
        // contains elements
        // make a power of 2 or not
        if (isPowerOf2($ans))
            return true;
    }
    return false;
}

    // Driver Code
    $arr= array(12, 13, 7);
    $n = sizeof($arr) / sizeof($arr[0]);
    if (checkSubsequence($arr, $n))
        echo "YES";
    else
        echo "NO";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to check if Bitwise AND of any
// subset is power of two

var NUM_BITS = 32;

// Check for power of 2 or not
function isPowerOf2(num)
{
    return (num && !(num & (num - 1)));
}

// Check if there exist a subset whose bitwise AND
// is power of 2.
function checkSubsequence(arr, n)
{

    // if there is only one element in the set.
    if (n == 1)
       return isPowerOf2(arr[0]);

    // Finding a number with all bit sets.
    var total = 0;
    for (var i = 0; i < NUM_BITS; i++)
        total = total | (1 << i);

    // check all the positions at which the bit is set.
    for (var i = 0; i < NUM_BITS; i++) {

        var ans = total;
        for (var j = 0; j < n; j++) {

            // include all those elements whose
            // i-th bit is set
            if (arr[j] & (1 << i))
                ans = ans & arr[j];
        }

        // check for the set contains elements
        // make a power of 2 or not
        if (isPowerOf2(ans))
            return true;
    }
    return false;
}

// Driver Program
var arr = [ 12, 13, 7 ];
var n = arr.length;
if (checkSubsequence(arr, n))
    document.write("YES<br>");
else
    document.write("NO<br>");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
YES
```

**参考:**
[https://stackoverflow . com/questions/35990794/如果我们做某个子集的所有元素的子集，然后输出](https://stackoverflow.com/questions/35990794/subset-of-array-a-in-which-if-we-do-and-of-all-elements-of-that-subset-then-outp)