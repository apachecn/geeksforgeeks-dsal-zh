# 检查数字是偶数还是奇数，给出数字和基数

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数字是偶数或奇数，则取其位数和基数的基数/](https://www.geeksforgeeks.org/check-if-the-number-is-even-or-odd-whose-digits-and-base-radix-is-given/)

给定一个大小为 **N** 的数组**arr【】**，该数组代表一个数字的位数和一个整数 **r** ，该整数是给定数字的基数(基数)，即**N = arr[N–1]* r<sup>0</sup>+arr[N–2]* r<sup>1</sup>+…+a[0]* r<sup>N–1</sup>**。任务是找出给定的数字是奇数还是偶数。
**举例:**

> **输入:** arr[] = {1，0}，r = 2
> **输出:**偶数
> (10)<sub>2</sub>=(2)<sub>10</sub>
> T11】输入: arr[] = {1，2，3，4，5，6，7，8，9}，r = 10
> **输出:**奇数

**天真法:**最简单的方法是将数字乘以相应的基数幂来计算数字 n。但是由于位数可以是 10 <sup>5</sup> 的数量级，这种方法不适用于大型 n.
**高效方法:**有两种可能。

1.  如果 **r 为偶数**，则最终答案取决于最后一位数字，即**arr[n–1]**。
2.  如果 **r 是奇数**那么我们要数奇数位数。如果奇数位数是偶数，那么和就是偶数。否则总和就是奇数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if the number
// represented by arr[] is even in base r
bool isEven(int arr[], int n, int r)
{

    // If the base is even, then
    // the last digit is checked
    if (r % 2 == 0) {
        if (arr[n - 1] % 2 == 0)
            return true;
    }

    // If base is odd, then the
    // number of odd digits are checked
    else {

        // To store the count of odd digits
        int oddCount = 0;
        for (int i = 0; i < n; ++i) {
            if (arr[i] % 2 != 0)
                oddCount++;
        }
        if (oddCount % 2 == 0)
            return true;
    }

    // Number is odd
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int r = 2;

    if (isEven(arr, n, r))
        cout << "Even";
    else
        cout << "Odd";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns true if the number
// represented by arr[] is even in base r
static boolean isEven(int arr[], int n, int r)
{

    // If the base is even, then
    // the last digit is checked
    if (r % 2 == 0)
    {
        if (arr[n - 1] % 2 == 0)
            return true;
    }

    // If base is odd, then the
    // number of odd digits are checked
    else {

        // To store the count of odd digits
        int oddCount = 0;
        for (int i = 0; i < n; ++i) {
            if (arr[i] % 2 != 0)
                oddCount++;
        }
        if (oddCount % 2 == 0)
            return true;
    }

    // Number is odd
    return false;
}

// Driver code
public static void main (String[] args)
{

    int arr[] = { 1, 0 };
    int n = arr.length;
    int r = 2;

    if (isEven(arr, n, r))

        System.out.println ("Even");
    else

        System.out.println("Odd");
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if the number
# represented by arr[] is even in base r
def isEven(arr, n, r):

    # If the base is even, then
    # the last digit is checked
    if (r % 2 == 0):
        if (arr[n - 1] % 2 == 0):
            return True

    # If base is odd, then the
    # number of odd digits are checked
    else:
        # To store the count of odd digits
        oddCount = 0
        for i in range(n):
            if (arr[i] % 2 != 0):
                oddCount += 1
        if (oddCount % 2 == 0):
            return True

    # Number is odd
    return False

# Driver code
if __name__ == '__main__':
    arr = [1, 0]
    n = len(arr)
    r = 2

    if (isEven(arr, n, r)):
        print("Even")
    else:
        print("Odd")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the number
// represented by arr[] is even in base r
static bool isEven(int []arr, int n, int r)
{

    // If the base is even, then
    // the last digit is checked
    if (r % 2 == 0)
    {
        if (arr[n - 1] % 2 == 0)
            return true;
    }

    // If base is odd, then the
    // number of odd digits are checked
    else
    {

        // To store the count of odd digits
        int oddCount = 0;
        for (int i = 0; i < n; ++i)
        {
            if (arr[i] % 2 != 0)
                oddCount++;
        }
        if (oddCount % 2 == 0)
            return true;
    }

    // Number is odd
    return false;
}

// Driver code
public static void Main ()
{

    int []arr = { 1, 0 };
    int n = arr.Length;
    int r = 2;

    if (isEven(arr, n, r))

        Console.WriteLine ("Even");
    else

        Console.WriteLine("Odd");
}
}

// This code is contributed by anuj_67...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function that returns true if the number
// represented by arr[] is even in base r
function isEven($arr, $n, $r)
{

    // If the base is even, then
    // the last digit is checked
    if ($r % 2 == 0)
    {
        if ($arr[$n - 1] % 2 == 0)
            return true;
    }

    // If base is odd, then the
    // number of odd digits are checked
    else
    {

        // To store the count of odd digits
        $oddCount = 0;
        for ($i = 0; $i < $n; ++$i)
        {
            if ($arr[$i] % 2 != 0)
                $oddCount++;
        }
        if ($oddCount % 2 == 0)
            return true;
    }

    // Number is odd
    return false;
}

    // Driver code
    $arr = array( 1, 0 );
    $n = Count($arr);
    $r = 2;

    if (isEven($arr, $n, $r))
        echo "Even";
    else
        echo "Odd";

// This code is contributed by andrew1234
?>
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    // Function that returns true if the number
    // represented by arr[] is even in base r
    function isEven(arr, n, r)
    {

        // If the base is even, then
        // the last digit is checked
        if (r % 2 == 0)
        {
            if (arr[n - 1] % 2 == 0)
                return true;
        }

        // If base is odd, then the
        // number of odd digits are checked
        else
        {

            // To store the count of odd digits
            let oddCount = 0;
            for (let i = 0; i < n; ++i)
            {
                if (arr[i] % 2 != 0)
                    oddCount++;
            }
            if (oddCount % 2 == 0)
                return true;
        }

        // Number is odd
        return false;
    }

    let arr = [ 1, 0 ];
    let n = arr.length;
    let r = 2;

    if (isEven(arr, n, r))

        document.write("Even");
    else
        document.write("Odd");

</script>
```

**Output:** 

```
Even
```