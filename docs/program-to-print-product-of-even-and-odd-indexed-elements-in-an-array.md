# 打印数组中偶数和奇数索引元素的乘积的程序

> 原文:[https://www . geeksforgeeks . org/程序打印偶数和奇数索引数组元素的乘积/](https://www.geeksforgeeks.org/program-to-print-product-of-even-and-odd-indexed-elements-in-an-array/)

给定一个整数数组。任务是编写一个程序，分别找到偶数和奇数索引位置的元素乘积。
**注**:数组考虑基于 0 的索引。也就是说，数组中第一个元素的索引为零。
T4【示例】T5:

```
Input : arr = {1, 2, 3, 4, 5, 6}
Output : Even Index Product : 15
         Odd Index Product : 48
Explanation: Here, N = 6 so there will be 3 even 
index positions and 3 odd index positions in the array
Even = 1 * 3 * 5 = 15
Odd =  2 * 4 * 6 = 48

Input : arr = {10, 20, 30, 40, 50, 60, 70}
Output : Even Index Product : 105000
         Odd Index Product : 48000
Explanation: Here, n = 7 so there will be 3 odd
index positions and 4 even index positions in an array
Even = 10 * 30 * 50 * 70 = 1050000
Odd = 20 * 40 * 60 = 48000 
```

遍历数组，保留两个变量**偶数**和**奇数**分别存储元素乘积和奇偶索引。遍历时，检查当前索引是偶数还是奇数，即(i%2)是否为零。如果当前元素与偶数索引积相乘，则与奇数索引积相乘。
以下是上述方法的实施:

## C++

```
// CPP program to find product of elements
// at even and odd index positions separately
#include <iostream>
using namespace std;

// Function to calculate product
void EvenOddProduct(int arr[], int n)
{
    int even = 1;
    int odd = 1;

    for (int i = 0; i < n; i++) {

        // Loop to find even, odd product
        if (i % 2 == 0)
            even *= arr[i];
        else
            odd *= arr[i];
    }

    cout << "Even Index Product : " << even << endl;
    cout << "Odd Index Product : " << odd;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    EvenOddProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of elements
// at even and odd index positions separately

class GFG
{

    // Function to calculate product
    static void EvenOddProduct(int arr[], int n)
    {
        int even = 1;
        int odd = 1;

        for (int i = 0; i < n; i++) {

            // Loop to find even, odd product
            if (i % 2 == 0)
                even *= arr[i];
            else
                odd *= arr[i];
        }

        System.out.println("Even Index Product : " + even);
        System.out.println("Odd Index Product : " + odd);
    }

    // Driver Code
    public static void main(String []args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int n = arr.length;

        EvenOddProduct(arr, n);

    }

   // This code is contributed by ihritik
}
```

## 蟒蛇 3

```
# Python3 program to find product of elements
# at even and odd index positions separately

# Function to calculate product
def EvenOddProduct(arr, n):

    even = 1 
    odd = 1 

    for i in range (0,n):

        # Loop to find even, odd product
        if (i % 2 == 0):
            even *= arr[i] 
        else:
            odd *= arr[i] 

    print("Even Index Product : " , even) 
    print("Odd Index Product : " , odd) 

# Driver Code

arr =   1, 2, 3, 4, 5, 6   
n = len(arr)

EvenOddProduct(arr, n) 

# This code is contributed by ihritik
```

## C#

```
// C# program to find product of elements
// at even and odd index positions separately

using System;
class GFG
{

    // Function to calculate product
    static void EvenOddProduct(int []arr, int n)
    {
        int even = 1;
        int odd = 1;

        for (int i = 0; i < n; i++) {

            // Loop to find even, odd product
            if (i % 2 == 0)
                even *= arr[i];
            else
                odd *= arr[i];
        }

        Console.WriteLine("Even Index Product : " + even);
        Console.WriteLine("Odd Index Product : " + odd);
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5, 6 };
        int n = arr.Length;

        EvenOddProduct(arr, n);

    }

   // This code is contributed by ihritik
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to find product of elements
// at even and odd index positions separately

// Function to calculate product
function EvenOddProduct($arr, $n)
{
    $even = 1;
    $odd = 1 ;

    for($i=0;$i<$n;$i++)
    {
        // Loop to find even, odd product
        if ($i % 2 == 0)
            $even *= $arr[$i];
        else
            $odd *= $arr[$i];

    }
    echo "Even Index Product: " .$even;
    echo "\n";
    echo "Odd Index Product: "  .$odd; 

}
// Driver Code

$arr =   array(1, 2, 3, 4, 5, 6) ;  
$n = sizeof($arr);

EvenOddProduct($arr, $n);

// This code is contributed by ihritik

?>
```

## java 描述语言

```
<script>

// Javascript program to find product of elements
// at even and odd index positions separately

// Function to calculate product
function EvenOddProduct(arr, n)
{
    let even = 1;
    let odd = 1;

    for (let i = 0; i < n; i++) {

        // Loop to find even, odd product
        if (i % 2 == 0)
            even *= arr[i];
        else
            odd *= arr[i];
    }

    document.write("Even Index Product : " + even + "<br>");
    document.write("Odd Index Product : " + odd);
}

// Driver Code

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;

    EvenOddProduct(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Even Index Product : 15
Odd Index Product : 48
```

**时间复杂度:** O(n)