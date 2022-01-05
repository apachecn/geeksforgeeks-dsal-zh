# 所有子阵列的按位“与”之和

> 原文:[https://www . geeksforgeeks . org/所有子数组的按位求和/](https://www.geeksforgeeks.org/sum-of-bitwise-and-of-all-subarrays/)

给定一个由 N 个正整数组成的数组，求该数组中所有可能的子数组的和。

**示例:**

```
Input : arr[] = {1, 5, 8}
Output : 15
Bit-wise AND of {1} = 1
Bit-wise AND of {1, 5} = 1
Bit-wise AND of {1, 5, 8} = 0 
Bit-wise AND of {5} = 5
Bit-wise AND of {5, 8} = 0
Bit-wise AND of {8} = 8

Sum = 1 + 1 + 0 + 5 + 0 + 8 =  15

Input : arr[] =  {7, 1, 1, 5}
Output : 20 
```

**简单解法**:一个简单的解法就是生成所有的子数组，将所有子数组的 and 值相加。平均而言，找到子阵列的“与”值需要线性时间，因此，整体时间复杂度为 0(n<sup>3</sup>)。

**高效解:**为了更好的理解，我们假设一个元素的任意一位用变量‘I’表示，变量‘sum’用来存储最终的和。
这里的想法是，我们将尝试使用第 i <sup>个</sup>位集来查找 AND 值的数量(具有按位 and( &)的子数组)。让我们假设，有 S <sub>i</sub> 数量的子阵列，其中 i <sup>第</sup>位被设置。例如，i <sup>第</sup>位，总和可以更新为总和+= (2 <sup>i</sup> * S)。
我们将任务分解为多个步骤。在每一步中，我们将试图找到第 I<sup>位设置的“与”值的数量。为此，我们将简单地迭代数组，并找到具有第 i <sup>位集的连续段的数量及其长度。对于长度为“l”的每个这样的段，sum 的值可以更新为 sum += (2 <sup>i</sup> * l * (l + 1))/2。
由于对于每一位，我们都在执行 O(N)次迭代，并且由于最多有 log(max(A))位，假设 max(A) =数组中的最大值，这种方法的时间复杂度将为 O(N*log(max(A))。</sup></sup>

下面是上述想法的实现:

## C++

```
// CPP program to find sum of bitwise AND
// of all subarrays

#include <iostream>
#include <vector>
using namespace std;

// Function to find the sum of
// bitwise AND of all subarrays
int findAndSum(int arr[], int n)
{
    // variable to store
    // the final sum
    int sum = 0;

    // multiplier
    int mul = 1;

    for (int i = 0; i < 30; i++) {
        // variable to check if
        // counting is on
        bool count_on = 0;

        // variable to store the
        // length of the subarrays
        int l = 0;

        // loop to find the contiguous
        // segments
        for (int j = 0; j < n; j++) {
            if ((arr[j] & (1 << i)) > 0)
                if (count_on)
                    l++;
                else {
                    count_on = 1;
                    l++;
                }

            else if (count_on) {
                sum += ((mul * l * (l + 1)) / 2);
                count_on = 0;
                l = 0;
            }
        }

        if (count_on) {
            sum += ((mul * l * (l + 1)) / 2);
            count_on = 0;
            l = 0;
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
int main()
{

    int arr[] = { 7, 1, 1, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findAndSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of bitwise AND
// of all subarrays
class GFG
{

// Function to find the sum of
// bitwise AND of all subarrays
static int findAndSum(int []arr, int n)
{
    // variable to store
    // the final sum
    int sum = 0;

    // multiplier
    int mul = 1;

    for (int i = 0; i < 30; i++)
    {
        // variable to check if
        // counting is on
        boolean count_on = false;

        // variable to store the
        // length of the subarrays
        int l = 0;

        // loop to find the contiguous
        // segments
        for (int j = 0; j < n; j++)
        {
            if ((arr[j] & (1 << i)) > 0)
                if (count_on)
                    l++;
                else
                {
                    count_on = true;
                    l++;
                }

            else if (count_on)
            {
                sum += ((mul * l * (l + 1)) / 2);
                count_on = false;
                l = 0;
            }
        }

        if (count_on)
        {
            sum += ((mul * l * (l + 1)) / 2);
            count_on = false;
            l = 0;
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 7, 1, 1, 5 };
    int n = arr.length;

    System.out.println(findAndSum(arr, n));
}
}

// This code is contributed
// by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to find Sum of
# bitwise AND of all subarrays
import math as mt

# Function to find the Sum of
# bitwise AND of all subarrays
def findAndSum(arr, n):

    # variable to store the final Sum
    Sum = 0

    # multiplier
    mul = 1

    for i in range(30):

        # variable to check if counting is on
        count_on = 0

        # variable to store the length
        # of the subarrays
        l = 0

        # loop to find the contiguous
        # segments
        for j in range(n):

            if ((arr[j] & (1 << i)) > 0):
                if (count_on):
                    l += 1
                else:
                    count_on = 1
                    l += 1

            elif (count_on):
                Sum += ((mul * l * (l + 1)) // 2)
                count_on = 0
                l = 0

        if (count_on):
            Sum += ((mul * l * (l + 1)) // 2)
            count_on = 0
            l = 0

        # updating the multiplier
        mul *= 2

    # returning the Sum
    return Sum

# Driver Code
arr = [7, 1, 1, 5]

n = len(arr)

print(findAndSum(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find sum of bitwise AND
// of all subarrays
using System;

class GFG
{

// Function to find the sum of
// bitwise AND of all subarrays
static int findAndSum(int []arr, int n)
{
    // variable to store
    // the final sum
    int sum = 0;

    // multiplier
    int mul = 1;

    for (int i = 0; i < 30; i++)
    {
        // variable to check if
        // counting is on
        bool count_on = false;

        // variable to store the
        // length of the subarrays
        int l = 0;

        // loop to find the contiguous
        // segments
        for (int j = 0; j < n; j++)
        {
            if ((arr[j] & (1 << i)) > 0)
                if (count_on)
                    l++;
                else
                {
                    count_on = true;
                    l++;
                }

            else if (count_on)
            {
                sum += ((mul * l * (l + 1)) / 2);
                count_on = false;
                l = 0;
            }
        }

        if (count_on)
        {
            sum += ((mul * l * (l + 1)) / 2);
            count_on = false;
            l = 0;
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
public static void Main()
{
    int []arr = { 7, 1, 1, 5 };
    int n = arr.Length;

    Console.Write(findAndSum(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of bitwise
// AND of all subarrays

// Function to find the sum of
// bitwise AND of all subarrays
function findAndSum($arr, $n)
{
    // variable to store the
    // final sum
    $sum = 0;

    // multiplier
    $mul = 1;

    for ($i = 0; $i < 30; $i++)
    {

        // variable to check if
        // counting is on
        $count_on = 0;

        // variable to store the
        // length of the subarrays
        $l = 0;

        // loop to find the contiguous
        // segments
        for ($j = 0; $j < $n; $j++)
        {
            if (($arr[$j] & (1 << $i)) > 0)
                if ($count_on)
                    $l++;
                else
                {
                    $count_on = 1;
                    $l++;
                }

            else if ($count_on)
            {
                $sum += (($mul * $l * ($l + 1)) / 2);
                $count_on = 0;
                $l = 0;
            }
        }

        if ($count_on)
        {
            $sum += (($mul * $l * ($l + 1)) / 2);
            $count_on = 0;
            $l = 0;
        }

        // updating the multiplier
        $mul *= 2;
    }

    // returning the sum
    return $sum;
}

// Driver Code
$arr = array( 7, 1, 1, 5 );

$n = sizeof($arr);

echo findAndSum($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of bitwise AND
// of all subarrays

// Function to find the sum of
// bitwise AND of all subarrays
function findAndSum(arr, n)
{
    // variable to store
    // the final sum
    var sum = 0;

    // multiplier
    var mul = 1;

    for (var i = 0; i < 30; i++) {
        // variable to check if
        // counting is on
        var count_on = 0;

        // variable to store the
        // length of the subarrays
        var l = 0;

        // loop to find the contiguous
        // segments
        for (var j = 0; j < n; j++) {
            if ((arr[j] & (1 << i)) > 0)
                if (count_on)
                    l++;
                else {
                    count_on = 1;
                    l++;
                }

            else if (count_on) {
                sum += ((mul * l * (l + 1)) / 2);
                count_on = 0;
                l = 0;
            }
        }

        if (count_on) {
            sum += ((mul * l * (l + 1)) / 2);
            count_on = 0;
            l = 0;
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
var arr = [ 7, 1, 1, 5 ];
var n = arr.length;
document.write( findAndSum(arr, n));

</script>
```

**Output:** 

```
20
```

**时间复杂度** : O(N*log(max(A))
**辅助空间:** O(1)