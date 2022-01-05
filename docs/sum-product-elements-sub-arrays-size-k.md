# 大小为 k 的子阵列所有元素的乘积之和

> 原文:[https://www . geesforgeks . org/sum-product-elements-子数组-size-k/](https://www.geeksforgeeks.org/sum-product-elements-sub-arrays-size-k/)

给定一个数组和一个数字 k，任务是计算大小为 k 的子数组的所有元素的乘积之和。
**示例:**

```
Input : arr[] = {1, 2, 3, 4, 5, 6} 
                k = 3
Output : 210
Consider all subarrays of size k
1*2*3 = 6
2*3*4 = 24
3*4*5 = 60
4*5*6 = 120
6 + 24 + 60 + 120 = 210

Input : arr[] = {1, -2, 3, -4, 5, 6} 
            k = 2
Output : -10
Consider all subarrays of size k
1*-2 = -2
-2*3 = -6
3*-4 = -12
-4*5 = -20
5*6  =   30
-2 + -6 + -12 + -20+ 30 = -10
```

一种**天真的方法**是生成大小为 k 的所有子阵，并对子阵所有元素的乘积求和。
T3】

## C++

```
// C++ program to find the sum of
// product of all subarrays
#include <iostream>
using namespace std;

// Function to calculate the sum of product
int calcSOP(int arr[], int n, int k)
{
    // Initialize sum = 0
    int sum = 0;

    // Consider every subarray of size k
    for (int i = 0; i <= n - k; i++) {
        int prod = 1;

        // Calculate product of all elements
        // of current subarray
        for (int j = i; j < k + i; j++)
            prod *= arr[j];

        // Store sum of all the products
        sum += prod;
    }

    // Return sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << calcSOP(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// product of all subarrays

class GFG {
    // Method to calculate the sum of product
    static int calcSOP(int arr[], int n, int k)
    {
        // Initialize sum = 0
        int sum = 0;

        // Consider every subarray of size k
        for (int i = 0; i <= n - k; i++) {
            int prod = 1;

            // Calculate product of all elements
            // of current subarray
            for (int j = i; j < k + i; j++)
                prod *= arr[j];

            // Store sum of all the products
            sum += prod;
        }

        // Return sum
        return sum;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int k = 3;

        System.out.println(calcSOP(arr, arr.length, k));
    }
}
```

## 蟒蛇 3

```
# python program to find the sum of
# product of all subarrays

# Function to calculate the sum of product
def calcSOP(arr, n, k):

    # Initialize sum = 0
    sum = 0

    # Consider every subarray of size k
    for i in range(0, (n-k)+1):
        prod = 1

        # Calculate product of all elements
        # of current subarray
        for j in range(i, k+i):
            prod = int(prod * arr[j])

        # Store sum of all the products
        sum = sum + prod

    # Return sum
    return sum

#Driver code
arr = [ 1, 2, 3, 4, 5, 6 ]
n = len(arr)
k = 3
print(calcSOP(arr, n, k))

# This code is contributed by Sam007
```

## C#

```
// C# program to find the sum of
// product of all subarrays
using System;

public class GFG {

    // Method to calculate the sum of product
    static int calcSOP(int[] arr, int n, int k)
    {
        // Initialize sum = 0
        int sum = 0;

        // Consider every subarray of size k
        for (int i = 0; i <= n - k; i++) {
            int prod = 1;

            // Calculate product of all elements
            // of current subarray
            for (int j = i; j < k + i; j++)
                prod *= arr[j];

            // Store sum of all the products
            sum += prod;
        }

        // Return sum
        return sum;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = {1, 2, 3, 4, 5, 6};
        int k = 3;

        Console.WriteLine(calcSOP(arr, arr.Length, k));
    }
}

// This code is contributed by Sam007
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-4">PHP</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-4" data-code-lang="php"></gfg-panel>

```
 <?php
// PHP program to find the sum of
// product of all subarrays

// Function to calculate
// the sum of product
function calcSOP($arr, $n, $k)
{

    // Initialize sum = 0
    $sum = 0;

    // Consider every subarray 
    // of size k
    for ($i = 0; $i <= $n - $k; $i++)
    {
        $prod = 1;

        // Calculate product of all 
        // elements of current subarray
        for ($j = $i; $j < $k + $i; $j++)
            $prod *= $arr[$j];

        // Store sum of all 
        // the products
        $sum += $prod;
    }

    // Return sum
    return $sum;
}

    // Driver code
    $arr = array( 1, 2, 3, 4, 5, 6 );
    $n = count($arr);
    $k = 3;

    echo calcSOP($arr, $n, $k);

// This code is contributed by Sam007
?> 
```

## java 描述语言

```
<script>
// Javascript program to find the sum of
// product of all subarrays

// Function to calculate
// the sum of product
function calcSOP(arr, n, k) {

    // Initialize sum = 0
    let sum = 0;

    // Consider every subarray
    // of size k
    for (let i = 0; i <= n - k; i++) {
        let prod = 1;

        // Calculate product of all
        // elements of current subarray
        for (let j = i; j < k + i; j++)
            prod *= arr[j];

        // Store sum of all
        // the products
        sum += prod;
    }

    // Return sum
    return sum;
}

// Driver code
let arr = new Array(1, 2, 3, 4, 5, 6);
let n = arr.length;
let k = 3;

document.write(calcSOP(arr, n, k));

// This code is contributed by gfgking
</script>
```

输出:

```
210
```

时间复杂度:O(nk)
一个**高效的方法**就是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)的概念。
1-考虑大小为 k 的第一个子阵列/窗口，做元素的乘积并加到 total_sum。

```
 for (i=0; i < k; i++)
       prod = prod * arr[i];
```

2-现在，通过使用滑动窗口概念，从产品中移除窗口的第一个元素，并将下一个元素添加到窗口中。即

```
for (i =k ; i < n; i++)
 {
     // Removing first element from product  
     prod = prod / arr[i-k]; 

     //  Adding current element to the product
     prod = prod * arr[i];  
     sum += prod;
 }
```

3-返回总和

## C++

```
// C++ program to find the sum of
// product of all subarrays
#include <iostream>
using namespace std;

    // Method to calculate the sum of product
    int calcSOP(int arr[], int n, int k)
    {
        // Initialize sum = 0 and prod = 1
        int sum = 0, prod = 1;

        // Consider first subarray of size k
        // Store the products of elements
        for (int i = 0; i < k; i++)
            prod *= arr[i];

        // Add the product to the sum
        sum += prod;

        // Consider every subarray of size k
        // Remove first element and add current
        // element to the window
        for (int i = k; i < n; i++) {

            // Divide by the first element
            // of previous subarray/ window
            // and product with the current element
            prod = (prod / arr[i - k]) * arr[i];

            // Add current product to the sum
            sum += prod;
        }

        // Return sum
        return sum;
    }

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << calcSOP(arr, n, k);
    return 0;
}

// This code is contributed by avijitmondal1998.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// product of all subarrays

class GFG {
    // Method to calculate the sum of product
    static int calcSOP(int arr[], int n, int k)
    {
        // Initialize sum = 0 and prod = 1
        int sum = 0, prod = 1;

        // Consider first subarray of size k
        // Store the products of elements
        for (int i = 0; i < k; i++)
            prod *= arr[i];

        // Add the product to the sum
        sum += prod;

        // Consider every subarray of size k
        // Remove first element and add current
        // element to the window
        for (int i = k; i < n; i++) {

            // Divide by the first element
            // of previous subarray/ window
            // and product with the current element
            prod = (prod / arr[i - k]) * arr[i];

            // Add current product to the sum
            sum += prod;
        }

        // Return sum
        return sum;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int k = 3;

        System.out.println(calcSOP(arr, arr.length, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# product of all subarrays

# Function to calculate the sum of product
def calcSOP(arr, n, k):

    # Initialize sum = 0 and prod = 1
    sum = 0
    prod = 1

    # Consider first subarray of size k
    # Store the products of elements
    for i in range(k):
        prod *= arr[i]

    # Add the product to the sum
    sum += prod

    # Consider every subarray of size k
    # Remove first element and add current
    # element to the window
    for i in range(k, n, 1):

        # Divide by the first element of
        #  previous subarray/ window and
        # product with the current element
        prod = (prod / arr[i - k]) * arr[i]

        # Add current product to the sum
        sum += prod

    # Return sum
    return int(sum)

# Drivers code
arr = [1, 2, 3, 4, 5, 6]
n = len(arr)
k = 3

print(calcSOP(arr, n, k))

# This code is contributed 29AjayKumar
```

## C#

```
// C# program to find the sum of
// product of all subarrays
using System;

public class GFG {

    // Method to calculate the sum of product
    static int calcSOP(int[] arr, int n, int k)
    {
        // Initialize sum = 0 and prod = 1
        int sum = 0, prod = 1;

        // Consider first subarray of size k
        // Store the products of elements
        for (int i = 0; i < k; i++)
            prod *= arr[i];

        // Add the product to the sum
        sum += prod;

        // Consider every subarray of size k
        // Remove first element and add current
        // element to the window
        for (int i = k; i < n; i++) {

            // Divide by the first element
            // of previous subarray/ window
            // and product with the current element
            prod = (prod / arr[i - k]) * arr[i];

            // Add current product to the sum
            sum += prod;
        }

        // Return sum
        return sum;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int k = 3;

        // Function calling
        Console.WriteLine(calcSOP(arr, arr.Length, k));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// php program to find the sum of
// product of all subarrays

// Function to calculate the sum of product
function calcSOP($arr, $n, $k)
{
    // Initialize sum = 0 and prod = 1
    $sum = 0;
    $prod = 1;

    // Consider first subarray of size k
    // Store the products of elements
    for ($i = 0; $i < $k; $i++)
        $prod *= $arr[$i];

    // Add the product to the sum
    $sum += $prod;

    // Consider every subarray of size k
    // Remove first element and add current
    // element to the window
    for ($i = $k; $i < $n; $i++) {

        // Divide by the first element
        // of previous subarray/ window
        // and product with the current element
        $prod = ($prod / $arr[$i - $k]) * $arr[$i];

        // Add current product to the sum
        $sum += $prod;
    }

    // Return sum
    return $sum;
}

// Drivers code
    $arr = array( 1, 2, 3, 4, 5, 6 );
    $n = count($arr);
    $k = 3;

    echo calcSOP($arr, $n, $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

function calcSOP(arr,n,k)
    {
        // Initialize sum = 0 and prod = 1
        let sum = 0, prod = 1;

        // Consider first subarray of size k
        // Store the products of elements
        for (let i = 0; i < k; i++)
            prod *= arr[i];

        // Add the product to the sum
        sum += prod;

        // Consider every subarray of size k
        // Remove first element and add current
        // element to the window
        for (let i = k; i < n; i++) {

            // Divide by the first element
            // of previous subarray/ window
            // and product with the current element
            prod = (Math.floor(prod / arr[i - k])) * arr[i];

            // Add current product to the sum
            sum += prod;
        }

        // Return sum
        return sum;
    }

    // Driver method

        let arr= [1, 2, 3, 4, 5, 6 ];
        let k = 3;

        document.write(calcSOP(arr, arr.length, k));

    // This code is contributed by Potta Lokesh

    </script>
```

**输出:**

```
210
```

**时间复杂度:** O(n)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。