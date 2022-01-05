# 用所有其他元素的总和替换数组中的每个元素

> 原文:[https://www . geeksforgeeks . org/用所有其他元素的总和替换数组中的每个元素/](https://www.geeksforgeeks.org/replace-every-element-of-the-array-by-sum-of-all-other-elements/)

给定一个大小为 N 的数组，任务是找到加密的数组。加密数组是通过用剩余数组元素的和替换原始数组的每个元素获得的，即

> 对于每个 I，
> arr[I]= sumOfArrayElements–arr[I]

**例:**

```
Input:  arr[] = {5, 1, 3, 2, 4} 
Output: 10 14 12 13 11
Original array {5, 1, 3, 2, 4}
Encrypted array is obtained as:
= {1+3+2+4, 5+3+2+4, 5+1+2+4, 5+1+3+4, 5+1+3+2}
= {10, 14, 12, 13, 11}
Each element of original array is replaced by the 
sum of the remaining array elements.  

Input: arr[] = {6, 8, 32, 12, 14, 10, 25 }
Output: 101 99 75 95 93 97 82 
```

这个问题类似于[从加密数组(其他元素之和的数组)中找到原始数组。](https://www.geeksforgeeks.org/find-original-array-encrypted-array-array-sums-elements/)
**进场:**

1.  求数组所有元素的和。
2.  遍历数组并将 **arr[i]** 替换为 **sum-arr[i]** 。

## C++

```
// C++ implementation to find encrypted array
// from the original array
#include <bits/stdc++.h>
using namespace std;

// Finds and prints the elements of the encrypted
// array
void findEncryptedArray(int arr[], int n)
{
    // total sum of elements
    // of original array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // calculating and displaying
    // elements of encrypted array
    for (int i = 0; i < n; i++)
        cout << (sum - arr[i]) << " ";
}

// Driver program
int main()
{
    int arr[] = { 5, 1, 3, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findEncryptedArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find encrypted
// array from the original  array

class GFG {
    // Finds and prints the elements
    // of the encrypted array
    static void findEncryptedArray(int arr[], int n)
    {
        // total sum of elements
        // of original array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // calculating and displaying
        // elements of encrypted array
        for (int i = 0; i < n; i++)
            System.out.print(sum - arr[i] + " ");
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 5, 1, 3, 2, 4 };
        int N = arr.length;
        findEncryptedArray(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation
# to find encrypted array
# from the original array

# Finds and prints the elements
# of the encrypted array
def findEncryptedArray(arr, n) :
    sum = 0

    # total sum of elements
    # of original array
    for i in range(n) :
        sum += arr[i]

    # calculating and displaying
    # elements of encrypted array
    for i in range(n) :
        print(sum - arr[i], end = " ")

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 1, 3, 2, 4]
    N = len(arr)

    # function calling
    findEncryptedArray(arr, N)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation to find
// encrypted array from the
// original array
using System;

class GFG
{
// Finds and prints the elements
// of the encrypted array
static void findEncryptedArray(int []arr,
                               int n)
{
    // total sum of elements
    // of original array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // calculating and displaying
    // elements of encrypted array
    for (int i = 0; i < n; i++)
        Console.Write(sum - arr[i] + " ");
}

// Driver Code
public static void Main()
{
    int []arr = { 5, 1, 3, 2, 4 };
    int N = arr.Length;
    findEncryptedArray(arr, N);
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find encrypted array
// from the original array

// Finds and prints the
// elements of the encrypted
// array
function findEncryptedArray(&$arr, $n)
{
    // total sum of elements
    // of original array
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // calculating and displaying
    // elements of encrypted array
    for ($i = 0; $i < $n; $i++)
        echo ($sum - $arr[$i]) . " ";
}

// Driver Code
$arr = array(5, 1, 3, 2, 4 );
$N = sizeof($arr);
findEncryptedArray($arr, $N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to find encrypted
// array from the original  array

    // Finds and prints the elements
    // of the encrypted array
    function findEncryptedArray(arr,n)
    {
        // total sum of elements
        // of original array
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += arr[i];

        // calculating and displaying
        // elements of encrypted array
        for (let i = 0; i < n; i++)
            document.write(sum - arr[i] + " ");
    }

    // Driver program
    let arr=[5, 1, 3, 2, 4 ];
    let N = arr.length;
    findEncryptedArray(arr, N);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
10 14 12 13 11
```

**时间复杂度:** O(n)