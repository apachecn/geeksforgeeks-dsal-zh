# 在 K 步中可以减少到 0 的最大数字 N

> 原文:[https://www . geeksforgeeks . org/最大数-n-哪些可以在 k 步中减少到 0/](https://www.geeksforgeeks.org/largest-number-n-which-can-be-reduced-to-0-in-k-steps/)

给定一个整数 **N** 。执行以下任务:

*   号码已记下。
*   从 **N** 中减去 **N** 的前导数字，结果值存储回 N 中
*   再次记下 **N** 的新值。
*   这个过程一直持续到 N 变成 0。最后， **0 记在最后**。

比如拿 **N = 13** 来说。在将 13 减少到 0 的过程中记下的数字将是:

*   Thirteen
*   13 – 1 = 12
*   12 – 1 = 11
*   11 – 1 = 10
*   10 – 1 = 9
*   9–9 = 0

给定一个整数 **K** ，这是如上所述将一个数 **N 减少到 0** 的过程中记下的数的总数，任务是找到起始数 **N** 的最大可能值。

**示例:**

> **输入:** k = 2
> **输出:** 9
> **说明:标注的数字= {9}**
> 
> *   减去前导数字:9–9 = 0。**标注的数字= {9，0 }**T2】
> 
> **输入:** k = 3
> **输出:** 10
> **说明:标注的数字= {10}**
> 
> *   减去前导数字:10–1 = 9。**标注的数字= {10，9}**
> *   减去前导数字:9–9 = 0。**标注的数字= {10，9，0}**

**方法:**想法是观察 N 的最大可能值将总是小于 10*K，因此，想法是在 K 到 10*K 的范围内应用二分搜索法，并寻找在 K 步中可以减少到 0 的最大值。
要找到最大可能的数字:

1.  初始化**左**至 **k** 和**右**至 **k*10** 。
2.  将**中间**初始化为**(左+右)/ 2** 。
3.  获取记下的数字的计数，将 *mid 转换为 0* ，并存储在 **len** 中。
4.  遵循分治法:当 **len** 不等于 **k** 时:
    *   将 mid 更新为当前**(左+右)/ 2** 。
    *   从**中间**开始计数。
    *   如果**计数**大于**中间**，则将**右侧**更新为**中间**。
    *   否则，更新**左**到**中**。
5.  现在， **mid** 有一个值会导致 **k** 整数被写下来。
6.  要找到最大的此类数字:
    *   而**计数**等于 **k** :
    *   如果当前**计数**不等于取**中间+1** 得到的**计数**，则断开
    *   否则，继续将**中间的**增加 1。
7.  如果将 **k** 整数写下来，中间的现在是最大可能的整数。

下面是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to return the first
// digit of a number.
int firstDigit(int n)
{
    // Remove last digit from number
    // till only one digit is left
    while (n >= 10) {
        n /= 10;
    }

    // return the first digit
    return n;
}

// Utility function that returns the count of numbers
// written down when starting from n
int getCount(int n)
{
    int count = 1;

    while (n != 0) {
        int leadDigit = firstDigit(n);
        n -= leadDigit;
        count++;
    }
    return count;
}

// Function to find the largest number N which
// can be reduced to 0 in K steps
int getLargestNumber(int k)
{
    int left = k;
    int right = k * 10;
    int mid = (left + right) / 2;

    // Get the sequence length of the mid point
    int len = getCount(mid);

    // Until k sequence length is reached
    while (len != k) {

        // Update mid point
        mid = (left + right) / 2;

        // Get count of the new mid point
        len = getCount(mid);

        if (len > k) {

            // Update right to mid
            right = mid;
        }
        else {

            // Update left to mid
            left = mid;
        }
    }

    // Increment mid point by one while count
    // is equal to k to get the maximum value
    // of mid point
    while (len == k) {

        if (len != getCount(mid + 1)) {
            break;
        }

        mid++;
    }

    return (mid);
}

// Driver Code
int main()
{
    int k = 3;

    cout << getLargestNumber(k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
import java.io.*;

class GFG
{

// Utility function to return the first
// digit of a number.
static int firstDigit(int n)
{
    // Remove last digit from number
    // till only one digit is left
    while (n >= 10)
    {
        n /= 10;
    }

    // return the first digit
    return n;
}

// Utility function that returns the count of numbers
// written down when starting from n
static int getCount(int n)
{
    int count = 1;

    while (n != 0)
    {
        int leadDigit = firstDigit(n);
        n -= leadDigit;
        count++;
    }
    return count;
}

// Function to find the largest number N which
// can be reduced to 0 in K steps
static int getLargestNumber(int k)
{
    int left = k;
    int right = k * 10;
    int mid = (left + right) / 2;

    // Get the sequence length of the mid point
    int len = getCount(mid);

    // Until k sequence length is reached
    while (len != k)
    {

        // Update mid point
        mid = (left + right) / 2;

        // Get count of the new mid point
        len = getCount(mid);

        if (len > k)
        {

            // Update right to mid
            right = mid;
        }
        else
        {

            // Update left to mid
            left = mid;
        }
    }

    // Increment mid point by one while count
    // is equal to k to get the maximum value
    // of mid point
    while (len == k)
    {

        if (len != getCount(mid + 1))
        {
            break;
        }

        mid++;
    }

    return (mid);
}

    // Driver Code
    public static void main (String[] args)
    {

        int k = 3;
        System.out.println (getLargestNumber(k));
    }
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 program to implement above approach

# Utility function to return the first
# digit of a number.
def firstDigit(n) :

    # Remove last digit from number
    # till only one digit is left
    while (n >= 10) :
        n //= 10;

    # return the first digit
    return n;

# Utility function that returns
# the count of numbers written
# down when starting from n
def getCount(n) :

    count = 1;

    while (n != 0) :
        leadDigit = firstDigit(n);
        n -= leadDigit;
        count += 1;

    return count;

# Function to find the largest number N
# which can be reduced to 0 in K steps
def getLargestNumber(k) :

    left = k;
    right = k * 10;
    mid = (left + right) // 2;

    # Get the sequence length of the mid point
    length = getCount(mid);

    # Until k sequence length is reached
    while (length != k) :

        # Update mid point
        mid = (left + right) // 2;

        # Get count of the new mid point
        length = getCount(mid);

        if (length > k) :

            # Update right to mid
            right = mid;

        else :

            # Update left to mid
            left = mid;

    # Increment mid point by one while count
    # is equal to k to get the maximum value
    # of mid point
    while (length == k) :

        if (length != getCount(mid + 1)) :
            break;

        mid += 1;

    return mid;

# Driver Code
if __name__ == "__main__" :

    k = 3;

    print(getLargestNumber(k));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to return the first
// digit of a number.
static int firstDigit(int n)
{
    // Remove last digit from number
    // till only one digit is left
    while (n >= 10)
    {
        n /= 10;
    }

    // return the first digit
    return n;
}

// Utility function that returns the count of numbers
// written down when starting from n
static int getCount(int n)
{
    int count = 1;

    while (n != 0)
    {
        int leadDigit = firstDigit(n);
        n -= leadDigit;
        count++;
    }
    return count;
}

// Function to find the largest number N which
// can be reduced to 0 in K steps
static int getLargestNumber(int k)
{
    int left = k;
    int right = k * 10;
    int mid = (left + right) / 2;

    // Get the sequence length of the mid point
    int len = getCount(mid);

    // Until k sequence length is reached
    while (len != k)
    {

        // Update mid point
        mid = (left + right) / 2;

        // Get count of the new mid point
        len = getCount(mid);

        if (len > k)
        {

            // Update right to mid
            right = mid;
        }
        else
        {

            // Update left to mid
            left = mid;
        }
    }

    // Increment mid point by one while count
    // is equal to k to get the maximum value
    // of mid point
    while (len == k)
    {

        if (len != getCount(mid + 1))
        {
            break;
        }

        mid++;
    }

    return (mid);
}

// Driver Code
public static void Main(String []args)
{
    int k = 3;

    Console.WriteLine( getLargestNumber(k));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement above approach

// Utility function to return the
// first digit of a number.
function firstDigit($n)
{

    // Remove last digit from number
    // till only one digit is left
    while ($n >= 10)
    {
        $n = (int)($n / 10);
    }

    // return the first digit
    return $n;
}

// Utility function that returns the
// count of numbers written down when
// starting from n
function getCount($n)
{
    $count = 1;

    while ($n != 0)
    {
        $leadDigit = firstDigit($n);
        $n -= $leadDigit;
        $count++;
    }
    return $count;
}

// Function to find the largest number N
// which can be reduced to 0 in K steps
function getLargestNumber($k)
{
    $left = $k;
    $right = $k * 10;
    $mid = (int)(($left + $right) / 2);

    // Get the sequence length
    // of the mid point
    $len = getCount($mid);

    // Until k sequence length is reached
    while ($len != $k)
    {

        // Update mid point
        $mid = (int)(($left + $right) / 2);

        // Get count of the new mid point
        $len = getCount($mid);

        if ($len > $k)
        {

            // Update right to mid
            $right = $mid;
        }
        else
        {

            // Update left to mid
            $left = $mid;
        }
    }

    // Increment mid point by one while count
    // is equal to k to get the maximum value
    // of mid point
    while ($len == $k)
    {
        if ($len != getCount($mid + 1))
        {
            break;
        }

        $mid++;
    }

    return ($mid);
}

// Driver Code
$k = 3;
echo(getLargestNumber($k));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

      // Utility function to return the first
    // digit of a number.
    function firstDigit(n)
    {
        // Remove last digit from number
        // till only one digit is left
        while (n >= 10)
        {
            n = parseInt(n / 10, 10);
        }

        // return the first digit
        return n;
    }

    // Utility function that returns the count of numbers
    // written down when starting from n
    function getCount(n)
    {
        let count = 1;

        while (n != 0)
        {
            let leadDigit = firstDigit(n);
            n -= leadDigit;
            count++;
        }
        return count;
    }

    // Function to find the largest number N which
    // can be reduced to 0 in K steps
    function getLargestNumber(k)
    {
        let left = k;
        let right = k * 10;
        let mid = parseInt((left + right) / 2, 10);

        // Get the sequence length of the mid point
        let len = getCount(mid);

        // Until k sequence length is reached
        while (len != k)
        {

            // Update mid point
            mid = parseInt((left + right) / 2, 10);

            // Get count of the new mid point
            len = getCount(mid);

            if (len > k)
            {

                // Update right to mid
                right = mid;
            }
            else
            {

                // Update left to mid
                left = mid;
            }
        }

        // Increment mid point by one while count
        // is equal to k to get the maximum value
        // of mid point
        while (len == k)
        {

            if (len != getCount(mid + 1))
            {
                break;
            }

            mid++;
        }

        return (mid);
    }

    let k = 3;

    document.write( getLargestNumber(k));

</script>
```

**Output:** 

```
10
```