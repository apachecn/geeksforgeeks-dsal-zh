# 用所有其他元素的乘积替换数组中的每个元素

> 原文:[https://www . geeksforgeeks . org/用所有其他元素的乘积替换数组中的每个元素/](https://www.geeksforgeeks.org/replace-every-element-of-the-array-by-product-of-all-other-elements/)

给定一个整数数组。用数组中所有其他元素的乘积替换每个元素。
**例:**

```
Input : arr[] = { 2, 3, 3, 5, 7 } 
Output : 315 210 210 126 90
```

**进场:**

*   首先，取数组中所有元素的乘积。
*   现在用除以元素的乘积替换每个元素。
*   打印修改后的数组。

以下是上述方法的实现:

## C++

```
// C++ program to Replace every element
// by the product of all other elements
#include "iostream"
using namespace std;

void ReplaceElements(int arr[], int n)
{
    int prod = 1;

    // Calculate the product of all the elements
    for (int i = 0; i < n; ++i) {
        prod *= arr[i];
    }

    // Replace every element product
    // of all other elements
    for (int i = 0; i < n; ++i) {
        arr[i] = prod / arr[i];
    }
}

int main()
{
    int arr[] = { 2, 3, 3, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Replace every element
// by the product of all other elements

class GFG{
static void ReplaceElements(int arr[], int n)
{
    int prod = 1;

    // Calculate the product of all the elements
    for (int i = 0; i < n; ++i) {
        prod *= arr[i];
    }

    // Replace every element product
    // of all other elements
    for (int i = 0; i < n; ++i) {
        arr[i] = prod / arr[i];
    }
}

public static void main(String[] args)
{
    int arr[] = { 2, 3, 3, 5, 7 };
    int n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i) {
        System.out.print(arr[i]+" ");
    }
    System.out.println("");

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to Replace every
# element by the product of all
# other elements

def ReplaceElements(arr, n):
    prod = 1

    # Calculate the product of
    # all the elements
    for i in range(n):
        prod *= arr[i]

    # Replace every element product
    # of all other elements
    for i in range(n) :
        arr[i] = prod // arr[i]

# Driver Code
if __name__ == "__main__":
    arr = [ 2, 3, 3, 5, 7 ]
    n = len(arr)

    ReplaceElements(arr, n)

    # Print the modified array.
    for i in range( n):
        print(arr[i], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to Replace every element
// by the product of all other elements
using System;

class GFG
{
static void ReplaceElements(int []arr, int n)
{
    int prod = 1;

    // Calculate the product of
    // all the elements
    for (int i = 0; i < n; ++i)
    {
        prod *= arr[i];
    }

    // Replace every element product
    // of all other elements
    for (int i = 0; i < n; ++i)
    {
        arr[i] = prod / arr[i];
    }
}

// Driver Code
static public void Main ()
{
    int []arr = { 2, 3, 3, 5, 7 };
    int n = arr.Length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i)
    {
        Console.Write(arr[i]+" ");
    }
    Console.WriteLine("");
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Replace every element
// by the product of all other elements

function ReplaceElements($arr, $n)
{
    $prod = 1;

    // Calculate the product of all
    // the elements
    for ($i = 0; $i < $n; ++$i)
    {
        $prod *= $arr[$i];
    }

    // Replace every element product
    // of all other elements
    for ($i = 0; $i < $n; ++$i)
    {
        $arr[$i] = (int)($prod / $arr[$i]);
    }
    return $arr;
}

// Driver Code
$arr = array( 2, 3, 3, 5, 7 );
$n = sizeof($arr);

$arr1 = ReplaceElements($arr, $n);

// Print the modified array.
for ($i = 0; $i < $n; ++$i)
{
    echo $arr1[$i] . " ";
}

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to Replace every element
    // by the product of all other elements

    function ReplaceElements(arr, n)
    {
        let prod = 1;

        // Calculate the product of
        // all the elements
        for (let i = 0; i < n; ++i)
        {
            prod *= arr[i];
        }

        // Replace every element product
        // of all other elements
        for (let i = 0; i < n; ++i)
        {
            arr[i] = parseInt(prod / arr[i], 10);
        }
    }

    let arr = [ 2, 3, 3, 5, 7 ];
    let n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (let i = 0; i < n; ++i)
    {
        document.write(arr[i]+" ");
    }

</script>
```

**输出:**

```
315 210 210 126 90
```

**时间复杂度**–O(N)