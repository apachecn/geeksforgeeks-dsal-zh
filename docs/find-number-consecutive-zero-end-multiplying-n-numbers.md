# n 个数相乘后求末尾连续零的个数

> 原文:[https://www . geesforgeks . org/find-number-continuous-zero-end-乘法-n-numbers/](https://www.geeksforgeeks.org/find-number-consecutive-zero-end-multiplying-n-numbers/)

给定一个有 n 个数字的数组。任务是将 n 个数字相乘后，在末尾打印连续零的个数。
**例:**

```
Input : arr[] = {100, 10}
Output : 3
Explanation : 100 x 10 = 1000,
3 zero's at the end.

Input : arr[] = {100, 10, 5, 25, 35, 14}
Output : 4
Explanation :
100 x 10 x 5 x 25 x 35 x 14 = 61250000,
4 zero's at the end
```

**天真的做法:**
先将所有数的倍数并存进串中(因为如果乘法数大如 2^64 那么它就给错了，所以把每一个倍数都存储在串中)然后再数零的个数。
**高效方法:**
首先计算 n 个数的 2 的因子，然后计算所有 n 个数的 5 的因子，然后打印最小的一个。
例如–

```
n_number's  | 2's factor | 5's factor 
100         |     2      |    2
10          |     1      |    1
5           |     0      |    1
25          |     0      |    2
35          |     0      |    1 
14          |     1      |    0
Total       |     4      |    7

we can take a minimum so there number of 
zero's is 4 
```

以下是上述方法的实现:

## C++

```
// CPP program to find the number of consecutive zero
// at the end after multiplying n numbers
#include<iostream>
using namespace std;

// Function to count two's factor
int two_factor(int n)
{   
    // Count number of 2s present in n
    int twocount = 0;
    while (n % 2 == 0)
    {
        twocount++;
        n = n / 2;
    }
    return twocount;
}

// Function to count five's factor
int five_factor(int n)
{
    int fivecount = 0;
    while (n % 5 == 0)
    {
        fivecount++;
        n = n / 5;
    }
    return fivecount;
}

// Function to count number of zeros
int find_con_zero(int arr[], int n)
{
    int twocount = 0;
    int fivecount = 0;
    for (int i = 0; i < n; i++) {

        // Count the two's factor of n number
        twocount += two_factor(arr[i]);

        // Count the five's factor of n number
        fivecount += five_factor(arr[i]);
    }

    // Return the minimum
    if (twocount < fivecount)
        return twocount;
    else
        return fivecount;
}

// Driver Code
int main()
{
    int arr[] = { 100, 10, 5, 25, 35, 14 };
    int n = 6;
    cout << find_con_zero(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of consecutive zero at the end
// after multiplying n numbers

public class GfG{

    // Function to count two's factor
    static int two_factor(int n)
    {    
        // Count number of 2s
        // present in n
        int twocount = 0;
        while (n % 2 == 0)
        {
            twocount++;
            n = n / 2;
        }
        return twocount;
    }

    // Function to count five's
    // factor
    static int five_factor(int n)
    {
        int fivecount = 0;
        while (n % 5 == 0)
        {
            fivecount++;
            n = n / 5;
        }
        return fivecount;
    }

    // Function to count number of zeros
    static int find_con_zero(int arr[], int n)
    {
        int twocount = 0;
        int fivecount = 0; 

        for (int i = 0; i < n; i++) {  

            // Count the two's factor
            // of n number
            twocount += two_factor(arr[i]);

            // Count the five's factor
            // of n number
            fivecount += five_factor(arr[i]);
        }

        // Return the minimum
        if (twocount < fivecount)
            return twocount;
        else
            return fivecount;
    }

    // driver function
    public static void main(String s[])
    {
        int arr[] = { 100, 10, 5, 25, 35, 14 };
        int n = 6;
        System.out.println(find_con_zero(arr, n));    
    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# Python3 code to find the number of consecutive zero
# at the end after multiplying n numbers

# Function to count two's factor
def two_factor( n ):

    # Count number of 2s present in n
    twocount = 0
    while n % 2 == 0:
        twocount+=1
        n =int( n / 2)
    return twocount

# Function to count five's factor
def five_factor( n ):
    fivecount = 0
    while n % 5 == 0:
        fivecount+=1
        n = int(n / 5)
    return fivecount

# Function to count number of zeros
def find_con_zero( arr, n ):
    twocount = 0
    fivecount = 0
    for i in range(n):

        # Count the two's factor of n number
        twocount += two_factor(arr[i])

        # Count the five's factor of n number
        fivecount += five_factor(arr[i])

    # Return the minimum
    if twocount < fivecount:
        return twocount
    else:
        return fivecount

# Driver Code
arr = [ 100, 10, 5, 25, 35, 14 ]
n = 6
print(find_con_zero(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find the number
// of consecutive zero at the end
// after multiplying n numbers
using System;

public class GfG {

    // Function to count two's factor
    static int two_factor(int n)
    {

        // Count number of 2s
        // present in n
        int twocount = 0;

        while (n % 2 == 0)
        {
            twocount++;
            n = n / 2;
        }

        return twocount;
    }

    // Function to count five's
    // factor
    static int five_factor(int n)
    {
        int fivecount = 0;

        while (n % 5 == 0)
        {
            fivecount++;
            n = n / 5;
        }

        return fivecount;
    }

    // Function to count number of zeros
    static int find_con_zero(int []arr, int n)
    {
        int twocount = 0;
        int fivecount = 0;

        for (int i = 0; i < n; i++) {

            // Count the two's factor
            // of n number
            twocount += two_factor(arr[i]);

            // Count the five's factor
            // of n number
            fivecount += five_factor(arr[i]);
        }

        // Return the minimum
        if (twocount < fivecount)
            return twocount;
        else
            return fivecount;
    }

    // driver function
    public static void Main()
    {

        int []arr = { 100, 10, 5, 25, 35, 14 };
        int n = 6;

        Console.WriteLine(find_con_zero(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number
// of consecutive zero at the end
// after multiplying n numbers

// Function to count two's factor
function two_factor($n)
{
    // Count number of
    // 2s present in n
    $twocount = 0;
    while ($n % 2 == 0)
    {
        $twocount++;
        $n = (int)($n / 2);
    }
    return $twocount;
}

// Function to count
// five's factor
function five_factor($n)
{
    $fivecount = 0;
    while ($n % 5 == 0)
    {
        $fivecount++;
        $n = (int)($n / 5);
    }
    return $fivecount;
}

// Function to count
// number of zeros
function find_con_zero($arr, $n)
{
    $twocount = 0;
    $fivecount = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Count the two's
        // factor of n number
        $twocount += two_factor($arr[$i]);

        // Count the five's
        // factor of n number
        $fivecount += five_factor($arr[$i]);
    }

    // Return the minimum
    if ($twocount < $fivecount)
        return $twocount;
    else
        return $fivecount;
}

// Driver Code
$arr= array(100, 10, 5,
            25, 35, 14);
$n = 6;
echo find_con_zero($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the number
// of consecutive zero at the end
// after multiplying n numbers

    // Function to count two's factor
    function two_factor(n)
    {    

        // Count number of 2s
        // present in n
        let twocount = 0;
        while (n % 2 == 0)
        {
            twocount++;
            n = n / 2;
        }
        return twocount;
    }

    // Function to count five's
    // factor
    function five_factor(n)
    {
        let fivecount = 0;
        while (n % 5 == 0)
        {
            fivecount++;
            n = n / 5;
        }
        return fivecount;
    }

    // Function to count number of zeros
    function find_con_zero(arr, n)
    {
        let twocount = 0;
        let fivecount = 0; 

        for (let i = 0; i < n; i++)
        {  

            // Count the two's factor
            // of n number
            twocount += two_factor(arr[i]);

            // Count the five's factor
            // of n number
            fivecount += five_factor(arr[i]);
        }

        // Return the minimum
        if (twocount < fivecount)
            return twocount;
        else
            return fivecount;
    }

// Driver code           
        let arr = [ 100, 10, 5, 25, 35, 14 ];
        let n = 6;
        document.write(find_con_zero(arr, n));

         // This code is contributed by code_hunt.
</script>
```

**输出:**

```
4
```