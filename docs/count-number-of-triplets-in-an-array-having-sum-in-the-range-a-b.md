# 计算数组中总和在[a，b]

范围内的三元组的数量

> 原文:[https://www . geeksforgeeks . org/count-数组中具有范围总和的三元组数量-a-b/](https://www.geeksforgeeks.org/count-number-of-triplets-in-an-array-having-sum-in-the-range-a-b/)

给定一个不同整数的数组和一个范围[a，b]，任务是计算具有在范围[a，b]内的和的三元组的数量。
**例:**

```
Input : arr[] = {8, 3, 5, 2}
        range = [7, 11]
Output : 1
There is only one triplet {2, 3, 5}
having sum 10 in range [7, 11].

Input : arr[] = {2, 7, 5, 3, 8, 4, 1, 9}
        range = [8, 16]
Output : 36
```

一种**天真的**方法是运行三个循环来逐个考虑所有的三元组。求每个三元组的和，如果和在给定的范围[a，b]内，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count triplets with
// sum that lies in given range [a, b].
#include <bits/stdc++.h>

using namespace std;

// Function to count triplets
int countTriplets(int arr[], int n, int a, int b)
{
    // Initialize result
    int ans = 0;

    // Fix the first element as A[i]
    for (int i = 0; i < n - 2; i++) {

        // Fix the second element as A[j]
        for (int j = i + 1; j < n - 1; j++) {

            // Now look for the third number
            for (int k = j + 1; k < n; k++)

                if (arr[i] + arr[j] + arr[k] >= a
                    && arr[i] + arr[j] + arr[k] <= b)
                    ans++;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, 5, 3, 8, 4, 1, 9 };
    int n = sizeof arr / sizeof arr[0];
    int a = 8, b = 16;
    cout << countTriplets(arr, n, a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count triplets
// with sum that lies in given
// range [a, b].
import java.util.*;

class GFG
{

// Function to count triplets
public static int countTriplets(int []arr, int n,
                                int a, int b)
{
    // Initialize result
    int ans = 0;

    // Fix the first
    // element as A[i]
    for (int i = 0; i < n - 2; i++)
    {

        // Fix the second
        // element as A[j]
        for (int j = i + 1; j < n - 1; j++)
        {

            // Now look for the
            // third number
            for (int k = j + 1; k < n; k++)
            {
                if (arr[i] + arr[j] + arr[k] >= a &&
                    arr[i] + arr[j] + arr[k] <= b)
                    {ans++;}
            }
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 7, 5, 3, 8, 4, 1, 9 };
    int n = arr.length;
    int a = 8, b = 16;
    System.out.println("" + countTriplets(arr, n,
                                        a, b));
}
}

// This code is contributed
// by Harshit Saini
```

## 蟒蛇 3

```
# Python3 program to count
# triplets with sum that
# lies in given range [a, b].

# Function to count triplets
def countTriplets(arr, n, a, b):

    # Initialize result
    ans = 0

    # Fix the first
    # element as A[i]
    for i in range(0, n - 2):

        # Fix the second
        # element as A[j]
        for j in range(i + 1, n - 1):

            # Now look for
            # the third number
            for k in range(j + 1, n):

                if ((arr[i] + arr[j] + arr[k] >= a)
                and (arr[i] + arr[j] + arr[k] <= b)):
                        ans += 1

    return ans

# Driver code
if __name__ == "__main__":

    arr = [ 2, 7, 5, 3, 8, 4, 1, 9 ]
    n = len(arr)
    a = 8; b = 16
    print(countTriplets(arr, n, a, b))

# This code is contributed
# by Harshit Saini
```

## C#

```
// C# program to count triplets
// with sum that lies in given
// range [a, b].
using System;

class GFG
{

// Function to count triplets
public static int countTriplets(int []arr, int n,
                                int a, int b)
{
    // Initialize result
    int ans = 0;

    // Fix the first
    // element as A[i]
    for (int i = 0;
            i < n - 2; i++)
    {

        // Fix the second
        // element as A[j]
        for (int j = i + 1;
                j < n - 1; j++)
        {

            // Now look for the
            // third number
            for (int k = j + 1;
                    k < n; k++)
            {
                if (arr[i] + arr[j] + arr[k] >= a &&
                    arr[i] + arr[j] + arr[k] <= b)
                    {ans++;}
            }
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = {2, 7, 5, 3, 8, 4, 1, 9};
    int n = arr.Length;
    int a = 8, b = 16;
    Console.WriteLine("" + countTriplets(arr, n,
                                        a, b));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count triplets with
// sum that lies in given range [a, b].

// Function to count triplets
function countTriplets($arr, $n, $a, $b)
{
    // Initialize result
    $ans = 0;

    // Fix the first element as A[i]
    for ($i = 0; $i < $n - 2; $i++)
    {

        // Fix the second element as A[j]
        for ($j = $i + 1; $j < $n - 1; $j++)
        {

            // Now look for the third number
            for ($k = $j + 1; $k < $n; $k++)

                if ($arr[$i] + $arr[$j] + $arr[$k] >= $a &&
                    $arr[$i] + $arr[$j] + $arr[$k] <= $b)
                    $ans++;
        }
    }

    return $ans;
}

// Driver Code
$arr = array( 2, 7, 5, 3, 8, 4, 1, 9 );
$n = sizeof($arr);
$a = 8; $b = 16;
echo countTriplets($arr, $n, $a, $b) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to count triplets with
// sum that lies in given range [a, b].

// Function to count triplets
function countTriplets( arr, n, a, b)
{
    // Initialize result
    var ans = 0;

    // Fix the first element as A[i]
    for (var i = 0; i < n - 2; i++) {

        // Fix the second element as A[j]
        for (var j = i + 1; j < n - 1; j++) {

            // Now look for the third number
            for (var k = j + 1; k < n; k++)

                if (arr[i] + arr[j] + arr[k] >= a
                    && arr[i] + arr[j] + arr[k] <= b)
                    ans++;
        }
    }

    return ans;
}

// Driver Code
var arr = [ 2, 7, 5, 3, 8, 4, 1, 9 ];
var n = arr.length;
var a = 8, b = 16;
document.write( countTriplets(arr, n, a, b) );

</script>
```

**Output:** 

```
36
```