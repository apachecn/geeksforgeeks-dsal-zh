# 各元素与其后各元素的乘积之和

> 原文:[https://www.geeksforgeeks.org/sum-product-element-element/](https://www.geeksforgeeks.org/sum-product-element-element/)

给定 n 个整数的数组 arr[]。任务是找出数组中每个元素与其后每个元素的乘积之和。换句话说，求每个 arr[i]与每个 arr[j]乘积的和，使得 j > i.
**例:**

```
Input : arr[] = {9, 3, 4, 2}
Output : 107
Sum of product of arr[0] with arr[1], 
arr[2], arr[3] is 9*3 + 9*4 + 9*2 = 81
Sum of product of arr[1] with arr[2], 
arr[3] is 3*4 + 3*2 = 18
Product of arr[2] with arr[3] is 4*2 = 8
Sum of all these sums is 81 + 18 + 8 = 107

Input : arr[] = {3, 5}
Output : 15
```

观察发现(p*a + p*b + …..+ p*y + p*z)等于 p*(a + b …..y + z)。
所以对于每个 I，0≤I≤n–2，我们必须计算 arr[i] * (arr[j] + arr[j+1] + …..+arr[n–2]+arr[n–1])，其中 j = i + 1，求这些的和。我们可以降低寻找的复杂度(arr[j] + arr[j+1] + …..+arr[n–2]+arr[n–1])，方法是预先计算数组的后缀和。
让 sum[]存储给定数组的后缀和，即 sum[i]有 arr[i] + arr[i+1] + …..+arr[n–2]+arr[n–1]。
所以，在预计算和[]之后，我们需要求 arr[I]*和[i + 1]的和，其中 0≤I≤n–2。
以下是本办法的实施:

## C++

```
// C++ Program to find sum of
// product of each element
// with each element after it
#include <bits/stdc++.h>
using namespace std;

// Return sum of product
// of each element with
// each element after it
int findSumofProduct(int arr[], int n)
{
    int sum[n];
    sum[n - 1] = arr[n - 1];

    // finding suffix sum
    for (int i = n - 2; i >= 0; i--)
        sum[i] = sum[i + 1] + arr[i];

    // finding the sum of product of
    // each element with suffix sum.
    int res = 0;
    for (int i = 0; i < n - 1; i++)
        res += (sum[i + 1] * arr[i]);

    return res;
}

// Driver Code
int main()
{
    int arr[] = {9, 3, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSumofProduct(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of product
// of each element with each element
// after it
class GFG {

    // Return sum of product of each
    // element with each element
    // after it
    static int findSumofProduct(int arr[],
                                    int n)
    {
        int sum[] = new int[n];
        sum[n - 1] = arr[n - 1];

        // finding suffix sum
        for (int i = n - 2; i >= 0; i--)
            sum[i] = sum[i + 1] + arr[i];

        // finding the sum of product of
        // each element with suffix sum.
        int res = 0;
        for (int i = 0; i < n - 1; i++)
            res += (sum[i + 1] * arr[i]);

        return res;
    }

    // Driver Program
    public static void main(String[] args)
    {

        int arr[] = { 9, 3, 4, 2 };
        int n = arr.length;

        System.out.println(
                findSumofProduct(arr, n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 Program to find sum of
# product of each element with
# each element after it

# Return sum of product of each
# element with each element after it
def findSumofProduct(arr, n):
    sum = [None for _ in range(n)]
    sum[n-1] = arr[n - 1]

    # finding suffix sum
    for i in range(n - 2, -1, -1):
        sum[i] = sum[i + 1] + arr[i]

    # finding the sum of product of
    # each element with suffix sum.
    res = 0
    for i in range(n - 1):
        res += sum[i + 1] * arr[i]
    return res

# Driver Code
arr = [9, 3, 4, 2]
n = len(arr)
print(findSumofProduct(arr, n))

# This code is contributed
# by SamyuktaSHegde
```

## C#

```
// C# Program to find sum of product
// of each element with each element
// after it
using System;

class GFG {

    // Return sum of product of each
    // element with each element
    // after it
    static int findSumofProduct(int[] arr,
                                    int n)
    {
        int[] sum = new int[n];
        sum[n - 1] = arr[n - 1];

        // finding suffix sum
        for (int i = n - 2; i >= 0; i--)
            sum[i] = sum[i + 1] + arr[i];

        // finding the sum of product of
        // each element with suffix sum.
        int res = 0;
        for (int i = 0; i < n - 1; i++)
            res += (sum[i + 1] * arr[i]);

        return res;
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = { 9, 3, 4, 2 };
        int n = arr.Length;

        Console.WriteLine(findSumofProduct(arr, n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// product of each element
// with each element after it

// Return sum of product
// of each element with
// each element after it
function findSumofProduct($arr, $n)
{

    $sum = array();
    $sum[$n - 1] = $arr[$n - 1];

    // finding suffix sum
    for ( $i = $n - 2; $i >= 0; $i--)
        $sum[$i] = $sum[$i + 1] + $arr[$i];

    // finding the sum of product of
    // each element with suffix sum.
    $res = 0;
    for ( $i = 0; $i < $n - 1; $i++)
        $res += ($sum[$i + 1] * $arr[$i]);

    return $res;
}

    // Driver Code
    $arr = array(9, 3, 4, 2);
    $n = count($arr);
    echo findSumofProduct($arr, $n);

// This code is contributed by anuJ_67.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find sum of
// product of each element
// with each element after it

// Return sum of product
// of each element with
// each element after it
function findSumofProduct(arr, n)
{
    let sum = new Array(n);
    sum[n - 1] = arr[n - 1];

    // finding suffix sum
    for (let i = n - 2; i >= 0; i--)
        sum[i] = sum[i + 1] + arr[i];

    // finding the sum of product of
    // each element with suffix sum.
    let res = 0;
    for (let i = 0; i < n - 1; i++)
        res += (sum[i + 1] * arr[i]);

    return res;
}

// Driver Code

    let arr = [9, 3, 4, 2];
    let n = arr.length;
    document.write(findSumofProduct(arr, n)
        + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
107
```

下面是求各元素与其后各元素乘积之和的优化代码:

## C++

```
// C++ Program to find sum of
// product of each element
// with each element after it
#include <bits/stdc++.h>
using namespace std;

// Return sum of product
// of each element with
// each element after it
int findSumofProduct(int arr[],
                     int n)
{
    int suffix_sum = arr[n - 1];

    // Finding product of array
    // elements and suffix sum.
    int res = 0;
    for (int i = n - 2; i >= 0; i--)
    {

        res += (suffix_sum * arr[i]);

        // finding suffix sum
        suffix_sum += arr[i];
    }

    return res;
}

// Driver Code
int main()
{
    int arr[] = {9, 3, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSumofProduct(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum
// of product of each
// element with each
// element after it
import java .io.*;
class GFG {

    // Return sum of product of
    // each element with each
    // element after it
    static int findSumofProduct(int[] arr,
                                int n)
    {
        int suffix_sum = arr[n - 1];

        // Finding product of array
        // elements and suffix sum.
        int res = 0;
        for (int i = n - 2; i >= 0; i--)
        {
            res += (suffix_sum * arr[i]);

            // finding suffix sum
            suffix_sum += arr[i];
        }

        return res;
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] arr = {9, 3, 4, 2};
        int n = arr.length;
        System.out.println(findSumofProduct(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to find sum of
# product of each element
# with each element after it

# Return sum of product
# of each element with
# each element after it
def findSumofProduct(arr, n):
    suffix_sum = arr[n - 1]

    # Finding product of array
    # elements and suffix sum.
    res = 0
    for i in range(n - 2, -1, -1):

        res += (suffix_sum * arr[i])

        # finding suffix sum
        suffix_sum += arr[i]

    return res;

# Driver Code
arr = [9, 3, 4, 2];
n = len(arr);
print(findSumofProduct(arr, n))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# Program to find sum
// of product of each
// element with each
// element after it
using System;

class GFG {

    // Return sum of product of
    // each element with each
    // element after it
    static int findSumofProduct(int[] arr,
                                int n)
    {
        int suffix_sum = arr[n - 1];

        // Finding product of array
        // elements and suffix sum.
        int res = 0;
        for (int i = n - 2; i >= 0; i--)
        {
            res += (suffix_sum * arr[i]);

            // finding suffix sum
            suffix_sum += arr[i];
        }

        return res;
    }

    // Driver code
    static public void Main()
    {
        int[] arr = {9, 3, 4, 2};
        int n = arr.Length;
        Console.WriteLine(findSumofProduct(arr, n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// product of each element
// with each element after it

// Return sum of product
// of each element with
// each element after it
function findSumofProduct($arr,
                          $n)
{
    $suffix_sum = $arr[$n - 1];

    // Finding product of array
    // elements and suffix sum.
    $res = 0;
    for ( $i = $n - 2; $i >= 0; $i--)
    {

        $res += ($suffix_sum * $arr[$i]);

        // finding suffix sum
        $suffix_sum += $arr[$i];
    }

    return $res;
}

    // Driver Code
    $arr = array(9, 3, 4, 2);
    $n = count($arr);
    echo findSumofProduct($arr, $n)

// This code is contributed by anuJ_67.
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find sum
    // of product of each
    // element with each
    // element after it

    // Return sum of product of
    // each element with each
    // element after it
    function findSumofProduct(arr, n)
    {
        let suffix_sum = arr[n - 1];

        // Finding product of array
        // elements and suffix sum.
        let res = 0;
        for (let i = n - 2; i >= 0; i--)
        {
            res += (suffix_sum * arr[i]);

            // finding suffix sum
            suffix_sum += arr[i];
        }

        return res;
    }

    let arr = [9, 3, 4, 2];
    let n = arr.length;
    document.write(findSumofProduct(arr, n));

</script>
```

**Output:** 

```
107
```