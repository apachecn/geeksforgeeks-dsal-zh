# 按降序重新排列 x 的倍数的所有数组元素

> 原文:[https://www . geeksforgeeks . org/rearray-数组中的所有元素都是 x 的倍数，按降序排列/](https://www.geeksforgeeks.org/rearrange-all-elements-of-array-which-are-multiples-of-x-in-decreasing-order/)

给定一个整数数组 **arr[]** 和一个整数 **x** ，任务是按照相对位置的降序对数组中是 **x** 倍数的所有元素进行排序，即其他元素的位置不得受到影响。

**示例:**

> **输入:** arr[] = {10，5，8，2，15}，x = 5
> **输出:** 15 10 8 2 5
> 我们将所有 5 的倍数(即 10，5 和 15)按相对位置降序重新排列，保持其他元素不变。
> 
> **输入:** arr[] = {100，12，25，50，5}，x = 5
> **输出:** 100 12 50 25 5

**进场:**

1.  遍历数组并检查该数是否是 x 的倍数。如果是，将其存储在向量中。
2.  然后，按降序排列向量。
3.  再次遍历数组，用向量元素逐个替换 5 的倍数的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort all the
// multiples of x from the
// array in decreasing order
void sortMultiples(int arr[], int n, int x)
{
    vector<int> v;

    // Insert all multiples of x to a vector
    for (int i = 0; i < n; i++)
        if (arr[i] % x == 0)
            v.push_back(arr[i]);

    // Sort the vector in descending
    sort(v.begin(), v.end(), std::greater<int>());

    int j = 0;

    // update the array elements
    for (int i = 0; i < n; i++) {
        if (arr[i] % x == 0)
            arr[i] = v[j++];
    }
}

// Utility function to print the array
void printArray(int arr[], int N)
{
    // Print the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 125, 3, 15, 6, 100, 5 };
    int x = 5;
    int n = sizeof(arr) / sizeof(arr[0]);

    sortMultiples(arr, n, x);

    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to sort all the
    // multiples of x from the
    // array in decreasing order
    static void sortMultiples(int arr[], int n, int x)
    {
        Vector<Integer> v = new Vector<Integer>();

        // Insert all multiples of x to a vector
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % x == 0)
            {
                v.add(arr[i]);
            }
        }

        // Sort the vector in descending
        Collections.sort(v, Collections.reverseOrder());

        int j = 0;

        // update the array elements
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % x == 0)
            {
                arr[i] = v.get(j++);
            }
        }
    }

    // Utility function to print the array
    static void printArray(int arr[], int N)
    {
        // Print the array
        for (int i = 0; i < N; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {125, 3, 15, 6, 100, 5};
        int x = 5;
        int n = arr.length;

        sortMultiples(arr, n, x);

        printArray(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to sort all the
# multiples of x from the
# array in decreasing order
def sortMultiples(arr, n, x) :
    v = []

    # Insert all multiples of x
    # to a vector
    for i in range(n) :
        if (arr[i] % x == 0) :
            v.append(arr[i])

    # Sort the vector in descending
    v.sort(reverse = True)
    j = 0

    # update the array elements
    for i in range(n) :
        if (arr[i] % x == 0) :
            arr[i] = v[j]
            j += 1

# Utility function to print the array
def printArray(arr, N) :

    # Print the array
    for i in range(N) :
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__" :

    arr= [ 125, 3, 15, 6, 100, 5 ]
    x = 5
    n = len(arr)

    sortMultiples(arr, n, x)

    printArray(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to sort all the
    // multiples of x from the
    // array in decreasing order
    static void sortMultiples(int []arr, int n, int x)
    {
        List<int> v = new List<int>();

        // Insert all multiples of x to a vector
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % x == 0)
            {
                v.Add(arr[i]);
            }
        }

        // Sort the vector in descending
        v.Sort();
        v.Reverse();

        int j = 0;

        // update the array elements
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % x == 0)
            {
                arr[i] = v[j++];
            }
        }
    }

    // Utility function to print the array
    static void printArray(int []arr, int N)
    {
        // Print the array
        for (int i = 0; i < N; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = {125, 3, 15, 6, 100, 5};
        int x = 5;
        int n = arr.Length;

        sortMultiples(arr, n, x);

        printArray(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to sort all the multiples
// of x from the array in decreasing order
function sortMultiples(&$arr, $n, $x)
{
    $v = array();

    // Insert all multiples of x to a vector
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] % $x == 0)
            array_push($v, $arr[$i]);

    // Sort the vector in descending
    rsort($v);

    $j = 0;

    // update the array elements
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] % $x == 0)
            $arr[$i] = $v[$j++];
    }
}

// Utility function to print the array
function printArray($arr, $N)
{
    // Print the array
    for ($i = 0; $i < $N; $i++)
    {
        echo $arr[$i] . " ";
    }
}

// Driver code
$arr = array(125, 3, 15, 6, 100, 5 );
$x = 5;
$n = sizeof($arr);

sortMultiples($arr, $n, $x);

printArray($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to sort all the
// multiples of x from the
// array in decreasing order
function sortMultiples(arr, n, x)
{
    var v = [];

    // Insert all multiples of x to a vector
    for(var i = 0; i < n; i++)
        if (arr[i] % x == 0)
            v.push(arr[i]);

    // Sort the vector in descending
    v.sort((a, b) => b - a);

    var j = 0;

    // update the array elements
    for(var i = 0; i < n; i++)
    {
        if (arr[i] % x == 0)
            arr[i] = v[j++];
    }
}

// Utility function to print the array
function printArray(arr, N)
{

    // Print the array
    for(var i = 0; i < N; i++)
    {
        document.write(arr[i] + "  ");
    }
}

// Driver code
var arr = [ 125, 3, 15, 6, 100, 5 ];
var x = 5;
var n = arr.length;

sortMultiples(arr, n, x);
printArray(arr, n);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
125 3 100 6 15 5
```

**时间复杂度:** O(n)