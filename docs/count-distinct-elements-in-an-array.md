# 计算数组中不同元素的数量

> 原文:[https://www . geesforgeks . org/count-distinct-elements in a array/](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

给定一个未排序的数组，计算其中所有不同的元素。
**例:**

```
Input :   arr[] = {10, 20, 20, 10, 30, 10}
Output : 3
There are three distinct elements 10, 20 and 30.

Input :   arr[] = {10, 20, 20, 10, 20}
Output : 2
```

一个**简单的解决方案**是运行两个循环。对于每个元素，检查它以前是否出现过。如果是，增加不同元素的计数。

## C++

```
// C++ program to count distinct elements
// in a given array
#include <iostream>
using namespace std;

int countDistinct(int arr[], int n)
{
    int res = 1;

    // Pick all elements one by one
    for (int i = 1; i < n; i++) {
        int j = 0;
        for (j = 0; j < i; j++)
            if (arr[i] == arr[j])
                break;

        // If not printed earlier, then print it
        if (i == j)
            res++;
    }
    return res;
}

// Driver program to test above function
int main()
{
    int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countDistinct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count distinct
// elements in a given array
class GFG
{

static int countDistinct(int arr[], int n)
{
    int res = 1;

    // Pick all elements one by one
    for (int i = 1; i < n; i++)
    {
        int j = 0;
        for (j = 0; j < i; j++)
            if (arr[i] == arr[j])
                break;

        // If not printed earlier,
        // then print it
        if (i == j)
            res++;
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 };
    int n = arr.length;
    System.out.println(countDistinct(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to count distinct
# elements in a given array
def countDistinct(arr, n):

    res = 1

    # Pick all elements one by one
    for i in range(1, n):
        j = 0
        for j in range(i):
            if (arr[i] == arr[j]):
                break

        # If not printed earlier, then print it
        if (i == j + 1):
            res += 1

    return res

# Driver Code
arr = [12, 10, 9, 45, 2, 10, 10, 45]
n = len(arr)
print(countDistinct(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count distinct
// elements in a given array
using System;

class GFG
{

static int countDistinct(int []arr, int n)
{
    int res = 1;

    // Pick all elements one by one
    for (int i = 1; i < n; i++)
    {
        int j = 0;
        for (j = 0; j < i; j++)
            if (arr[i] == arr[j])
                break;

        // If not printed earlier,
        // then print it
        if (i == j)
            res++;
    }
    return res;
}

// Driver code
public static void Main()
{
    int []arr = { 12, 10, 9, 45,
                  2, 10, 10, 45 };
    int n = arr.Length;
    Console.WriteLine(countDistinct(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count distinct elements
// in a given array
function countDistinct( &$arr, $n)
{
    $res = 1;

    // Pick all elements one by one
    for ( $i = 1; $i < $n; $i++)
    {

        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] == $arr[$j])
                break;

        // If not printed earlier,
        // then print it
        if ($i == $j)
            $res++;
    }
    return $res;
}

// Driver Code
$arr = array( 12, 10, 9, 45, 2, 10, 10, 45 );
$n = count($arr);
echo countDistinct($arr, $n);

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>

// JavaScript program to count distinct elements
// in a given array

function countDistinct(arr, n)
{
    let res = 1;

    // Pick all elements one by one
    for (let i = 1; i < n; i++) {
        let j = 0;
        for (j = 0; j < i; j++)
            if (arr[i] === arr[j])
                break;

        // If not printed earlier, then print it
        if (i === j)
            res++;
    }
    return res;
}

// Driver program to test above function
    let arr = [ 12, 10, 9, 45, 2, 10, 10, 45 ];
    let n = arr.length;
    document.write(countDistinct(arr, n));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output**

```
5
```