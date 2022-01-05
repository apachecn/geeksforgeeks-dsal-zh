# 由给定数组中每个元素与最大元素之差形成的数组

> 原文:[https://www . geeksforgeeks . org/array-由给定数组中最大元素的每个元素之差形成/](https://www.geeksforgeeks.org/array-formed-from-difference-of-each-element-from-the-largest-element-in-the-given-array/)

给定一个数组 **arr[]** ，任务是从给定数组中最大的元素中找出每个元素的差形成的数组。

**示例:**

> **输入:** arr[] = {3，6，9，2，6}
> **输出:** {6，3，0，7，3}
> **解释:**
> 数组最大元素= 9
> 因此 arr[i]与 9 的区别:
> 元素 1:9–3 = 6
> 元素 2:9–6 = 3
> 元素 3:9–9 = 0
> 元素 4:9–2 = 7
> 
> **输入:** arr[] = {7，2，5，6，3，1，6，9}
> **输出:** {2，7，4，3，6，8，3，0}

**逼近:**
找到数组中 n 个元素中最大的一个，并将其存储在一个最大的变量中。现在检查数组中最大元素和其他元素之间的差异。

下面是上述方法的实现:

## C++

```
// C++ program to find the array formed
// from the difference of each element
// from the largest element in the given array

#include <iostream>
using namespace std;
int difference(int arr[], int n)
{
    // Initializing current largest
    // as the first element.
    int largest = arr[0];
    int i;

    // For loop to compute
    // the largest element
    for (i = 0; i < n; i++) {

        // Checking if the current element
        // is greater than the defined largest
        if (largest < arr[i])
            largest = arr[i];
    }

    // For loop to replace the elements
    // in the array with the difference
    for (i = 0; i < n; i++)
        arr[i] = largest - arr[i];

    // For loop to print the elements
    for (i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 10, 5, 9, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    difference(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the array formed
// from the difference of each element
// from the largest element in the given array
import java.util.*;

class GFG
{
static void difference(int arr[], int n)
{
    // Initializing current largest
    // as the first element.
    int largest = arr[0];
    int i;

    // For loop to compute
    // the largest element
    for (i = 0; i < n; i++)
    {

        // Checking if the current element
        // is greater than the defined largest
        if (largest < arr[i])
            largest = arr[i];
    }

    // For loop to replace the elements
    // in the array with the difference
    for (i = 0; i < n; i++)
        arr[i] = largest - arr[i];

    // For loop to print the elements
    for (i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 10, 5, 9, 3, 2 };
    int n = arr.length;
    difference(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the array formed
# from the difference of each element
# from the largest element in the given array
def difference(arr, n):

    # Initializing current largest
    # as the first element.
    largest = arr[0];
    i = 0;

    # For loop to compute
    # the largest element
    for i in range(n):

        # Checking if the current element
        # is greater than the defined largest
        if (largest < arr[i]):
            largest = arr[i];

    # For loop to replace the elements
    # in the array with the difference
    for i in range(n):
        arr[i] = largest - arr[i];

    # For loop to print the elements
    for i in range(n):
        print(arr[i], end = " ");

# Driver code
if __name__ == '__main__':
    arr = [ 10, 5, 9, 3, 2 ];
    n = len(arr);
    difference(arr, n);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find the array formed
// from the difference of each element
// from the largest element in the given array
using System;

class GFG
{

static void difference(int []arr, int n)
{
    // Initializing current largest
    // as the first element.
    int largest = arr[0];
    int i;

    // For loop to compute
    // the largest element
    for (i = 0; i < n; i++)
    {

        // Checking if the current element
        // is greater than the defined largest
        if (largest < arr[i])
            largest = arr[i];
    }

    // For loop to replace the elements
    // in the array with the difference
    for (i = 0; i < n; i++)
        arr[i] = largest - arr[i];

    // For loop to print the elements
    for (i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 10, 5, 9, 3, 2 };
    int n = arr.Length;
    difference(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the array formed
// from the difference of each element
// from the largest element in the given array

function difference(arr, n)
{
    // Initializing current largest
    // as the first element.
    let largest = arr[0];
    let i;

    // For loop to compute
    // the largest element
    for (i = 0; i < n; i++)
    {

        // Checking if the current element
        // is greater than the defined largest
        if (largest < arr[i])
            largest = arr[i];
    }

    // For loop to replace the elements
    // in the array with the difference
    for (i = 0; i < n; i++)
        arr[i] = largest - arr[i];

    // For loop to prthe elements
    for (i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver code

let arr = [10, 5, 9, 3, 2];
let n = arr.length;
difference(arr, n);

</script>
```

**Output:** 

```
0 5 1 7 8
```