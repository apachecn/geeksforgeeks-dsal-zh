# 可以用 n 位数字排列形成的所有数字的总和

> 原文:[https://www . geesforgeks . org/sum-numbers-can-formed-排列-n-digits/](https://www.geeksforgeeks.org/sum-numbers-can-formed-permutations-n-digits/)

给定 n 个不同的数字(从 0 到 9)，求可以用这些数字构成的所有 n 个数字的和。假设允许使用以 0 开头的数字。

**示例:**

```
Input: 1 2 3
Output: 1332
Explanation
Numbers Formed: 123 , 132 , 312 , 213, 231 , 321
123 + 132 + 312 + 213 + 231 + 321 = 1332
```

可以用 n 位数字组成的总数是 n 位数字排列的总数，即阶乘(n)。现在，由于形成的数字是一个 n 位数字，每个数字将在从最低有效数字到最高有效数字的每个位置出现阶乘(n)/n 次。因此，一个位置的位数之和=(所有位数之和)*(阶乘(n)/n)。

```
Considering the example digits as 1 2 3

factorial(3)/3 = 2

Sum of digits at least significant digit = (1 + 2 + 3) * 2 = 12

Similarly sum of digits at tens, hundreds place is 12\. 
(This sum will contribute as 12 * 100)

Similarly sum of digits at tens, thousands place is 12\. 
(This sum will contribute as 12 * 1000)

Required sum of all numbers = 12 + (10 * 12) + (100 * 12) = 1332
```

## C++

```
// C++ program to find sun of numbers formed
// by all permutations of given set of digits
#include<stdio.h>

// function to calculate factorial of a number
int factorial(int n)
{
    int f = 1;
    if (n==0||n==1)
        return 1;
    for (int i=2; i<=n; i++)
        f = f*i;
    return f;
}

// Function to calculate sum of all numbers
int getSum(int arr[],int n)
{
    // calculate factorial
    int fact = factorial(n);

    // sum of all the given digits at different
    // positions is same and is going to be stored
    // in digitsum.
    int digitsum = 0;
    for (int i=0; i<n; i++)
        digitsum += arr[i];
    digitsum *= (fact/n);

    // Compute result (sum of all the numbers)
    int res = 0;
    for (int i=1, k=1; i<=n; i++)
    {
        res  += (k*digitsum);
        k = k*10;
    }

    return res;
}

// Driver program to test above function
int main()
{
    // n distinct digits
    int arr[] = {1, 2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Print sum of all the numbers formed
    printf("%d", getSum(arr, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum
// of numbers formed by all
// permutations of given set
// of digits
import java.io.*;

class GFG
{

// function to calculate
// factorial of a number
static int factorial(int n)
{
    int f = 1;
    if (n == 0|| n == 1)
        return 1;
    for (int i = 2; i <= n; i++)
        f = f * i;
    return f;
}

// Function to calculate
// sum of all numbers
static int getSum(int arr[], int n)
{
    // calculate factorial
    int fact = factorial(n);

    // sum of all the given
    // digits at different
    // positions is same and
    // is going to be stored
    // in digitsum.
    int digitsum = 0;
    for (int i = 0; i < n; i++)
        digitsum += arr[i];
    digitsum *= (fact / n);

    // Compute result (sum
    // of all the numbers)
    int res = 0;
    for (int i = 1, k = 1;
             i <= n; i++)
    {
        res += (k * digitsum);
        k = k * 10;
    }

    return res;
}

// Driver Code
public static void main (String[] args)
{

    // n distinct digits
    int arr[] = {1, 2, 3};
    int n = arr.length;

    // Print sum of all
    // the numbers formed
    System.out.println(getSum(arr, n));
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to find sun of
# numbers formed by all permutations
# of given set of digits

# function to calculate factorial
# of a number
def factorial(n):

    f = 1
    if (n == 0 or n == 1):
        return 1
    for i in range(2, n + 1):
        f = f * i
    return f

# Function to calculate sum
# of all numbers
def getSum(arr, n):

    # calculate factorial
    fact = factorial(n)

    # sum of all the given digits at
    # different positions is same and
    # is going to be stored in digitsum.
    digitsum = 0
    for i in range(n):
        digitsum += arr[i]
    digitsum *= (fact // n)

    # Compute result (sum of
    # all the numbers)
    res = 0
    i = 1
    k = 1
    while i <= n :
        res += (k * digitsum)
        k = k * 10
        i += 1

    return res

# Driver Code
if __name__ == "__main__":

    # n distinct digits
    arr = [1, 2, 3]
    n = len(arr)

    # Print sum of all the numbers formed
    print(getSum(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find sum
// of numbers formed by all
// permutations of given set
// of digits
using System;

class GFG
{

// function to calculate
// factorial of a number
static int factorial(int n)
{
    int f = 1;
    if (n == 0|| n == 1)
        return 1;
    for (int i = 2; i <= n; i++)
        f = f * i;
    return f;
}

// Function to calculate
// sum of all numbers
static int getSum(int []arr,
                  int n)
{
    // calculate factorial
    int fact = factorial(n);

    // sum of all the given
    // digits at different
    // positions is same and
    // is going to be stored
    // in digitsum.
    int digitsum = 0;
    for (int i = 0; i < n; i++)
        digitsum += arr[i];
    digitsum *= (fact / n);

    // Compute result (sum
    // of all the numbers)
    int res = 0;
    for (int i = 1, k = 1;
            i <= n; i++)
    {
        res += (k * digitsum);
        k = k * 10;
    }

    return res;
}

// Driver Code
static public void Main ()
{

    // n distinct digits
    int []arr = {1, 2, 3};
    int n = arr.Length;

    // Print sum of all
    // the numbers formed
    Console.WriteLine(getSum(arr, n));
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of numbers formed by all
// permutations of given set
// of digits function to
// calculate factorial of a number
function factorial($n)
{
    $f = 1;
    if ($n == 0||$n == 1)
        return 1;
    for ($i = 2; $i <= $n; $i++)
        $f = $f * $i;
    return $f;
}

// Function to calculate
// sum of all numbers
function getSum($arr,$n)
{
    // calculate factorial
    $fact = factorial($n);

    // sum of all the given
    // digits at different
    // positions is same and
    // is going to be stored
    // in digitsum.
    $digitsum = 0;
    for ($i = 0; $i < $n; $i++)
        $digitsum += $arr[$i];
    $digitsum *= ($fact / $n);

    // Compute result (sum
    // of all the numbers)
    $res = 0;
    for ($i = 1, $k = 1; $i <= $n; $i++)
    {
        $res += ($k * $digitsum);
        $k = $k * 10;
    }

    return $res;
}

// Driver Code

// n distinct digits
$arr = array(1, 2, 3);
$n = sizeof($arr);

// Print sum of all
// the numbers formed
echo getSum($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of
// numbers formed by all permutations
// of given set of digits

// Function to calculate
// factorial of a number
function factorial(n)
{
    let f = 1;

    if (n == 0 || n == 1)
        return 1;

    for (let i = 2; i <= n; i++)
        f = f * i;

    return f;
}

// Function to calculate
// sum of all numbers
function getSum(arr, n)
{

    // Calculate factorial
    let fact = factorial(n);

    // Sum of all the given
    // digits at different
    // positions is same and
    // is going to be stored
    // in digitsum.
    let digitsum = 0;
    for (let i = 0; i < n; i++)
        digitsum += arr[i];

    digitsum *= (fact / n);

    // Compute result (sum
    // of all the numbers)
    let res = 0;
    for(let i = 1, k = 1;
            i <= n; i++)
    {
        res += (k * digitsum);
        k = k * 10;
    }
    return res;
}

// Driver code

// n distinct digits
let arr = [1, 2, 3];
let n = arr.length;

// Print sum of all
// the numbers formed
document.write(getSum(arr, n));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
1332
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。