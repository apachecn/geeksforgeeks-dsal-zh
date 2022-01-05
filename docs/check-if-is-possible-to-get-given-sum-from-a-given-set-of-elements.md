# 检查是否有可能从给定的一组元素中得到给定的和

> 原文:[https://www . geeksforgeeks . org/check-如果可能，从给定的元素集中获取给定的总和/](https://www.geeksforgeeks.org/check-if-is-possible-to-get-given-sum-from-a-given-set-of-elements/)

给定一个数字数组和一个整数 x，通过给定数组的元素相加，找出是否有可能得到 x，我们可以多次选取一个元素。对于给定的数组，可以有许多求和查询。
**例:**

```
Input : arr[] = { 2, 3}
         q[]  = {8, 7}
Output : Yes Yes
Explanation : 
2 + 2 + 2 + 2 = 8
2 + 2 + 3 = 7
```

其思想是首先对给定的数组进行排序，然后使用类似于厄拉多塞的[筛的概念。首先取一个大尺寸的数组(它是 x 的最大尺寸)。最初在所有索引中保持零。在零索引处做 1(无论数组是什么，我们都可以得到零)。现在，遍历整个数组，将所有可能的值设为 1。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find if we can get given
// sum using elements of given array.
#include <bits/stdc++.h>
using namespace std;

// maximum size of x
const int MAX = 1000;

// to check whether x is possible or not
int ispossible[MAX];

void check(int arr[], int N)
{
    ispossible[0] = 1;
    sort(arr, arr + N);

    for (int i = 0; i < N; ++i) {
        int val = arr[i];

        // if it is already possible
        if (ispossible[val])
            continue;

        // make 1 to all it's next elements
        for (int j = 0; j + val < MAX; ++j)
            if (ispossible[j])
                ispossible[j + val] = 1;
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    check(arr, N);
    int x = 7;
    if (ispossible[x])
        cout << x << " is possible.";
    else
        cout << x << " is not possible.";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if we can get given
// sum using elements of given array.
import java.util.*;

class solution
{

// maximum size of x
int MAX = 1000;

// to check whether x is possible or not
static int []ispossible = new int[1000];
static void check(int[] arr, int N)
{

    ispossible[0] = 1;
    Arrays.sort(arr);

    for (int i = 0; i < N; ++i) {
        int val = arr[i];

        // if it is already possible
        if (ispossible[val] == 1)
            continue;

        // make 1 to all it's next elements
        for (int j = 0; j + val < 1000; ++j)
            if (ispossible[j]== 1)
                ispossible[j + val] = 1;
    }
}

// Driver code
public static void main(String args[])
{
    int[] arr = { 2, 3 };
    int N = arr.length;
    check(arr, N);
    int x = 7;
    if (ispossible[x]== 1)
        System.out.println(x+" is possible.");
    else
        System.out.println(x+" is not possible.");

}
}
// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 program to find if we can get given
# sum using elements of the given array.
def check(arr, N):

    ispossible[0] = 1
    arr.sort()

    for i in range(0, N):
        val = arr[i]

        # if it is already possible
        if ispossible[val]:
            continue

        # make 1 to all it's next elements
        for j in range(0, MAX - val):
            if ispossible[j]:
                ispossible[j + val] = 1

# Driver code
if __name__ == "__main__":

    arr = [2, 3]
    N = len(arr)

    # maximum size of x
    MAX = 1000

    # to check whether x is possible or not
    ispossible = [0] * MAX

    check(arr, N)
    x = 7

    if ispossible[x]:
        print(x, "is possible.")
    else:
        print(x, "is not possible.")

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to find if we can get given
// sum using elements of given array.
using System;

class GFG
{

// to check whether x is possible or not
static int []ispossible = new int[1000];
static void check(int[] arr, int N)
{

    ispossible[0] = 1;
    Array.Sort(arr);

    for (int i = 0; i < N; ++i)
    {
        int val = arr[i];

        // if it is already possible
        if (ispossible[val] == 1)
            continue;

        // make 1 to all it's next elements
        for (int j = 0; j + val < 1000; ++j)
            if (ispossible[j] == 1)
                ispossible[j + val] = 1;
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 3 };
    int N = arr.Length;
    check(arr, N);
    int x = 7;
    if (ispossible[x]== 1)
        Console.WriteLine(x + " is possible.");
    else
        Console.WriteLine(x + " is not possible.");
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if we can get given
// sum using elements of given array.

// maximum size of x
$MAX = 1000;

// to check whether x is possible or not
$ispossible[$MAX] = array();

function check($arr, $N)
{
    global $MAX;
    $ispossible[0] = 1;
    sort($arr, 0);

    for ($i = 0; $i < $N; ++$i)
    {
        $val = $arr[$i];

        // if it is already possible
        if ($ispossible[$val])
            continue;

        // make 1 to all it's next elements
        for ($j = 0; $j + $val < $MAX; ++$j)
            if ($ispossible[$j])
                $ispossible[$j + $val] = 1;
    }
}

// Driver code
$arr = array( 2, 3 );
$N = sizeof($arr);
check($arr, $N);
$x = 7;
if (ispossible[$x])
    echo $x . " is possible.";
else
    echo $x . " is not possible.";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to find if we can get given
// sum using elements of given array.

// maximum size of x
let MAX = 1000;

// to check whether x is possible or not
let ispossible = new Array(MAX);

function check(arr, N)
{
    ispossible[0] = 1;
    arr.sort();

    for (let i = 0; i < N; ++i)
    {
        val = arr[i];

        // if it is already possible
        if (ispossible[val])
            continue;

        // make 1 to all it's next elements
        for (let j = 0; j + val < MAX; ++j)
            if (ispossible[j])
                ispossible[j + val] = 1;
    }
}

// Driver code
let arr = new Array( 2, 3 );
let N = arr.length;
check(arr, N);
let x = 7;
if (ispossible[x])
    document.write(x + " is possible.");
else
    document.write(x + " is not possible.");

// This code is contributed
// by _sauraahb_jaiswal
</script>
```

**输出:**

```
7 is possible.
```