# 检查 N 个数的按位“或”是偶数还是奇数

> 原文:[https://www . geeksforgeeks . org/check-n-numbers 的按位或是偶数还是奇数/](https://www.geeksforgeeks.org/check-whether-bitwise-or-of-n-numbers-is-even-or-odd/)

给定一个包含 N 个数字的数组 arr[]。任务是检查给定 N 个数字的按位“或”是偶数还是奇数。
**例** :

```
Input : arr[] = { 2, 12, 20, 36, 38 }
Output : Even Bit-wise OR

Input : arr[] = { 3, 9, 12, 13, 15 }
Output : Odd Bit-wise OR
```

一个**简单的解决方法**是先找到给定 N 个数的 OR，然后检查这个 OR 是偶数还是奇数。
时间复杂度:O(N)
A **更好的解**是基于比特操作和数学事实。

*   任意两个偶数的按位“或”是偶数。

*   任意两个奇数的按位“或”是奇数。

*   偶数和奇数的按位“或”是奇数。

基于以上事实，可以推断，如果数组中至少存在一个奇数，则整个数组的按位“或”将是奇数，否则是偶数。
以下是上述方法的实现:

## C++

```
// C++ implementation to check whether
// bitwise OR of n numbers is even or odd
#include <bits/stdc++.h>
using namespace std;

// Function to check if bitwise OR
// of n numbers is even or odd
bool check(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        // if at least one odd number is found,
        // then the bitwise OR of all numbers will be odd
        if (arr[i] & 1)
            return true;
    }

    // Bitwise OR is an odd number
    return false;
}

// Driver Code
int main()
{
    int arr[] = { 3, 9, 12, 13, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (check(arr, n))
        cout << "Odd Bit-wise OR";
    else
        cout << "Even Bit-wise OR";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// bitwise OR of n numbers is even or odd
class GFG
{

// Function to check if bitwise OR
// of n numbers is even or odd
static boolean check(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        // if at least one odd number is
        // found, then the bitwise OR of
        // all numbers will be odd
        if (arr[i] % 2 == 1)
        {
            return true;
        }
    }

    // Bitwise OR is an odd number
    return false;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = {3, 9, 12, 13, 15};
    int n = arr.length;

    if (check(arr, n))
    {
        System.out.println("Odd Bit-wise OR");
    }
    else
    {
        System.out.println("Even Bit-wise OR");
    }
}
}

// This code is contributed
// by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to check whether
# bitwise OR of n numbers is even or odd

# Function to check if bitwise OR
# of n numbers is even or odd
def check(arr,n):
    for i in range(n):

        # if at least one odd number is found,
        # then the bitwise OR of all numbers
        # will be odd
        if arr[i] & 1:
            return True

    # Bitwise OR is an odd number
    return False

# Driver code
if __name__=='__main__':
    arr = [3, 9, 12, 13, 15]
    n = len(arr)
    if check(arr,n):
        print("Odd Bit-wise OR")
    else:
        print("Even Bit-wise OR")

# This code is contributed by
# Shrikant13
```

## C#

```
// C# implementation to check whether
// bitwise OR of n numbers is even or odd
using System;

class GFG
{

// Function to check if bitwise OR
// of n numbers is even or odd
static bool check(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        // if at least one odd number is
        // found, then the bitwise OR of
        // all numbers will be odd
        if (arr[i] % 2 == 1)
        {
            return true;
        }
    }

    // Bitwise OR is an odd number
    return false;
}

// Driver Code
public static void Main()
{
    int []arr = {3, 9, 12, 13, 15};
    int n = arr.Length;

    if (check(arr, n))
    {
        Console.WriteLine("Odd Bit-wise OR");
    }
    else
    {
        Console.WriteLine("Even Bit-wise OR");
    }
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHp implementation to check whether
// bitwise OR of n numbers is even or odd

// Function to check if bitwise OR
// of n numbers is even or odd

function  check($arr, $n)
{
    for ($i = 0; $i < $n; $i++) {
        // if at least one odd number is found,
        // then the bitwise OR of all numbers will be odd
        if ($arr[$i] & 1)
            return true;
    }

    // Bitwise OR is an odd number
    return false;
}

// Driver Code

    $arr = array (3, 9, 12, 13, 15 );
     $n = sizeof($arr) / sizeof($arr[0]);

    if (check($arr, $n))
         echo  "Odd Bit-wise OR";
    else
        echo "Even Bit-wise OR";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to check whether
// bitwise OR of n numbers is even or odd

// Function to check if bitwise OR
// of n numbers is even or odd
function check(arr, n)
{
    for (let i = 0; i < n; i++)
    {

        // if at least one odd number is found,
        // then the bitwise OR of all numbers will be odd
        if (arr[i] & 1)
            return true;
    }

    // Bitwise OR is an odd number
    return false;
}

// Driver Code
    let arr = [ 3, 9, 12, 13, 15 ];
    let n = arr.length;

    if (check(arr, n))
        document.write("Odd Bit-wise OR");
    else
        document.write("Even Bit-wise OR");

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
Odd Bit-wise OR
```

**时间复杂度**:最差情况下为 O(N)。