# 求偶和的子阵个数

> 原文:[https://www . geesforgeks . org/find-number-subarrays-偶数-sum/](https://www.geeksforgeeks.org/find-number-subarrays-even-sum/)

给定一个数组，求其和为偶数的子数组的个数。

**示例:**

```
Input : arr[] = {1, 2, 2, 3, 4, 1} 
Output : 9

There are possible subarrays with even
sum. The subarrays are 
1) {1, 2, 2, 3}  Sum = 8
2) {1, 2, 2, 3, 4}  Sum = 12
3) {2}  Sum = 2 (At index 1)
4) {2, 2}  Sum = 4
5) {2, 2, 3, 4, 1}  Sum = 12
6) {2}  Sum = 2 (At index 2)
7) {2, 3, 4, 1} Sum = 10
8) {3, 4, 1}  Sum = 8
9) {4}  Sum = 4 
```

**O(n <sup>2</sup> )时间和 O(1)空间方法【蛮力】**
我们可以简单地生成所有可能的子数组，并找出其中所有元素的和是否为偶数。如果是偶数，那么我们将计算该子阵列，否则忽略它。

## C++

```
/* C++ program to count number of sub-arrays
  whose sum is even using brute force
 Time Complexity - O(N^2)
 Space Complexity - O(1) */
#include<iostream>
using namespace std;

int countEvenSum(int arr[], int n)
{
    int result = 0;

    // Find sum of all subarrays and increment
    // result if sum is even
    for (int i=0; i<=n-1; i++)
    {
        int sum = 0;
        for (int j=i; j<=n-1; j++)
        {
            sum = sum + arr[j];
            if (sum % 2 == 0)
                    result++;
        }
    }

    return (result);
}

// Driver code
int main()
{
    int arr[] = {1, 2, 2, 3, 4, 1};
    int n = sizeof (arr) / sizeof (arr[0]);

    cout << "The Number of Subarrays with even"
            " sum is " << countEvenSum (arr, n);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of sub-arrays whose sum is
// even using brute force
// Time Complexity - O(N^2)
// Space Complexity - O(1)
import java.io.*;

class GFG
{
static int countEvenSum(int arr[],
                        int n)
{
    int result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is even
    for (int i = 0; i <= n - 1; i++)
    {
        int sum = 0;
        for (int j = i; j <= n - 1; j++)
        {
            sum = sum + arr[j];
            if (sum % 2 == 0)
                    result++;
        }
    }

    return (result);
}

// Driver code
public static void main (String[] args)
{
int arr[] = {1, 2, 2,
             3, 4, 1};
int n = arr.length;

System.out.print("The Number of Subarrays"+
                     " with even sum is ");

System.out.println(countEvenSum(arr, n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python 3 program to count number
# of sub-arrays whose sum is even
# using brute force
# Time Complexity - O(N^2)
# Space Complexity - O(1)

def countEvenSum(arr, n):
    result = 0

    # Find sum of all subarrays and
    # increment result if sum is even
    for i in range(0, n, 1):
        sum = 0
        for j in range(i, n, 1):
            sum = sum + arr[j]
            if (sum % 2 == 0):
                    result = result + 1

    return (result)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 2, 3, 4, 1]
    n = len(arr)
    print("The Number of Subarrays" ,
                  "with even sum is",
               countEvenSum (arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number
// of sub-arrays whose sum is
// even using brute force
// Time Complexity - O(N^2)
// Space Complexity - O(1)
using System;

class GFG
{
static int countEvenSum(int []arr,
                        int n)
{
    int result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is even
    for (int i = 0; i <= n - 1; i++)
    {
        int sum = 0;
        for (int j = i; j <= n - 1; j++)
        {
            sum = sum + arr[j];
            if (sum % 2 == 0)
                    result++;
        }
    }

    return (result);
}

// Driver code
static public void Main ()
{
    int []arr = {1, 2, 2,
                 3, 4, 1};
    int n = arr.Length;

    Console.Write("The Number of Subarrays"+
                      " with even sum is ");

    Console.WriteLine(countEvenSum(arr, n));
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of sub-arrays whose sum is
// even using brute force
// Time Complexity - O(N^2)
// Space Complexity - O(1)
function countEvenSum($arr, $n)
{
    $result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is even
    for ($i = 0; $i <= $n - 1; $i++)
    {
        $sum = 0;
        for ($j = $i; $j <= $n - 1; $j++)
        {
            $sum = $sum + $arr[$j];
            if ($sum % 2 == 0)
                    $result++;
        }
    }

    return ($result);
}

// Driver code
$arr = array(1, 2, 2, 3, 4, 1);
$n = sizeof ($arr);

echo "The Number of Subarrays ",
           "with even sum is " ,
        countEvenSum ($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count number
// of sub-arrays whose sum is
// even using brute force
// Time Complexity - O(N^2)
// Space Complexity - O(1)

function countEvenSum(arr,
                        n)
{
    let result = 0;

    // Find sum of all subarrays
    // and increment result if
    // sum is even
    for (let i = 0; i <= n - 1; i++)
    {
        let sum = 0;
        for (let j = i; j <= n - 1; j++)
        {
            sum = sum + arr[j];
            if (sum % 2 == 0)
                    result++;
        }
    }

    return (result);
}

// Driver Code

let arr = [1, 2, 2,
             3, 4, 1];
let n = arr.length;

document.write("The Number of Subarrays"+
                     " with even sum is ");

document.write(countEvenSum(arr, n));

</script>
```

**Output**

```
The Number of Subarrays with even sum is 9
```