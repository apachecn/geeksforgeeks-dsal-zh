# 所有子阵列的异或之和

> 原文:[https://www.geeksforgeeks.org/sum-of-xor-of-all-subarrays/](https://www.geeksforgeeks.org/sum-of-xor-of-all-subarrays/)

给定一个包含 N 个正整数的数组，任务是求该数组所有子数组的异或之和。
**例:**

```
Input : arr[] = {1, 3, 7, 9, 8, 7}
Output : 128

Input : arr[] = {3, 8, 13}
Output : 46

Explanation for second test-case:
XOR of {3} = 3
XOR of {3, 8} = 11
XOR of {3, 8, 13} = 6
XOR of {8} = 8
XOR of {8, 13} = 5
XOR of {13} = 13

Sum = 3 + 11 + 6 + 8 + 5 + 13 = 46
```

**简单的解决方案:**一个简单的解决方案是生成所有的子数组，然后遍历它们，找到所需的异或值，然后求和。这种方法的时间复杂度为 0(n<sup>3</sup>)。
**更好的解决方案:**更好的解决方案是使用前缀数组，即对于数组“arr[]”的每个索引“I”，创建一个前缀数组来存储从数组“arr[]”的左端到“arr[]”的 I<sup>元素的所有元素的异或。创建前缀数组需要一段时间。
现在，使用这个前缀数组，我们可以在 O(1)时间内找到任意子数组的 XOR 值。
我们可以使用公式
找到从索引 l 到 r 的异或</sup>

```
if l is not zero 
    XOR = prefix[r] ^ prefix[l-1]
else 
    XOR = prefix[r].
```

在这之后，我们要做的就是，总结一下，所有子数组的异或值。
由于子阵列的总数为 **(N <sup>2</sup> )** 的数量级，因此该方法的时间复杂度为 O(N <sup>2</sup> )。
**最佳解决方案:**为了更好的理解，我们假设一个元素的任意一位都用变量‘I’表示，变量‘sum’用来存储最终的和。
这里的想法是，我们将尝试用第 i <sup>个</sup>位集来寻找异或值的数量。让我们假设，有 S <sub>i</sub> 数量的子阵列，i <sup>第</sup>位被设置。对于，i <sup>第</sup>位，该和可以更新为**和+= (2 <sup>i</sup> * S)** 。
那么，问题是如何落实上述思路？
我们将任务分解为多个步骤。在每一步中，我们将尝试用第 i <sup>个</sup>位组找到异或值的数量。
现在，我们将每个步骤分解为子步骤。在每个子步骤中，我们将尝试从索引“j”(其中 j 在 0 到 n–1 之间变化)开始查找子阵列的数量，其中第 I<sup>位被设置为它们的异或值。因为，i <sup>第</sup>位将被设置，子阵列的奇数个元素应该在 i <sup>第</sup>位被设置。
对于所有的位，在变量 c_odd 中，我们将存储从 j = 0 开始的子阵列数量的计数，i <sup>第</sup>位设置在奇数个元素中。然后，我们将遍历数组的所有元素，在需要时更新 c_odd 的值。如果我们到达 i <sup>第</sup>位设置的元素‘j ’,我们将更新 c_odd 为**c _ odd =(n–j–c _ odd)**。这是因为，由于我们遇到了一个设置位，具有偶数个元素的 i **第**位设置的子阵列的数量将切换到具有奇数个元素的 i **第**位设置的子阵列的数量。
以下是本办法的实施:</sup> 

## C++

```
// C++ program to find the sum of XOR of
// all subarray of the array

#include <iostream>
#include <vector>
using namespace std;

// Function to calculate the sum of XOR
// of all subarrays
int findXorSum(int arr[], int n)
{
    // variable to store
    // the final sum
    int sum = 0;

    // multiplier
    int mul = 1;

    for (int i = 0; i < 30; i++) {

        // variable to store number of
        // sub-arrays with odd number of elements
        // with ith bits starting from the first
        // element to the end of the array
        int c_odd = 0;

        // variable to check the status
        // of the odd-even count while
        // calculating c_odd
        bool odd = 0;

        // loop to calculate initial
        // value of c_odd
        for (int j = 0; j < n; j++) {
            if ((arr[j] & (1 << i)) > 0)
                odd = (!odd);
            if (odd)
                c_odd++;
        }

        // loop to iterate through
        // all the elements of the
        // array and update sum
        for (int j = 0; j < n; j++) {
            sum += (mul * c_odd);

            if ((arr[j] & (1 << i)) > 0)
                c_odd = (n - j - c_odd);
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
    int arr[] = { 3, 8, 13 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findXorSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of XOR
// of all subarray of the array
import java.util.*;

class GFG
{
    // Function to calculate the sum of XOR
    // of all subarrays
    static int findXorSum(int arr[], int n)
    {
        // variable to store
        // the final sum
        int sum = 0;

        // multiplier
        int mul = 1;

        for (int i = 0; i < 30; i++)
        {

            // variable to store number of
            // sub-arrays with odd number of elements
            // with ith bits starting from the first
            // element to the end of the array
            int c_odd = 0;

            // variable to check the status
            // of the odd-even count while
            // calculating c_odd
            boolean odd = false;

            // loop to calculate initial
            // value of c_odd
            for (int j = 0; j < n; j++)
            {
                if ((arr[j] & (1 << i)) > 0)
                    odd = (!odd);
                if (odd)
                    c_odd++;
            }

            // loop to iterate through
            // all the elements of the
            // array and update sum
            for (int j = 0; j < n; j++)
            {
                sum += (mul * c_odd);

                if ((arr[j] & (1 << i)) > 0)
                    c_odd = (n - j - c_odd);
            }

            // updating the multiplier
            mul *= 2;
        }

        // returning the sum
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 8, 13 };
        int n = arr.length;

        System.out.println(findXorSum(arr, n));
    }
}

// This code is contributed by Rituraj Jain.
```

## 蟒蛇 3

```
# Python3 program to find the Sum of
# XOR of all subarray of the array

# Function to calculate the Sum of XOR
# of all subarrays
def findXorSum(arr, n):

    # variable to store the final Sum
    Sum = 0

    # multiplier
    mul = 1

    for i in range(30):

        # variable to store number of sub-arrays
        # with odd number of elements with ith
        # bits starting from the first element
        # to the end of the array
        c_odd = 0

        # variable to check the status of the
        # odd-even count while calculating c_odd
        odd = 0

        # loop to calculate initial
        # value of c_odd
        for j in range(n):
            if ((arr[j] & (1 << i)) > 0):
                odd = (~odd)
            if (odd):
                c_odd += 1

        # loop to iterate through all the
        # elements of the array and update Sum
        for j in range(n):
            Sum += (mul * c_odd)

            if ((arr[j] & (1 << i)) > 0):
                c_odd = (n - j - c_odd)

        # updating the multiplier
        mul *= 2

    # returning the Sum
    return Sum

# Driver Code
arr = [3, 8, 13]

n = len(arr)

print(findXorSum(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the sum of XOR of
// all subarray of the array
using System;

class GFG
{

// Function to calculate the sum
// of XOR of all subarrays
static int findXorSum(int []arr, int n)
{
    // variable to store
    // the final sum
    int sum = 0;

    // multiplier
    int mul = 1;

    for (int i = 0; i < 30; i++)
    {

        // variable to store number of sub-arrays
        // with odd number of elements  with ith
        // bits starting from the first element
        // to the end of the array
        int c_odd = 0;

        // variable to check the status
        // of the odd-even count while
        // calculating c_odd
        bool odd = false;

        // loop to calculate initial
        // value of c_odd
        for (int j = 0; j < n; j++)
        {
            if ((arr[j] & (1 << i)) > 0)
                odd = (!odd);
            if (odd)
                c_odd++;
        }

        // loop to iterate through
        // all the elements of the
        // array and update sum
        for (int j = 0; j < n; j++)
        {
            sum += (mul * c_odd);

            if ((arr[j] & (1 << i)) > 0)
                c_odd = (n - j - c_odd);
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
static void Main()
{
    int []arr = { 3, 8, 13 };

    int n = arr.Length;

    Console.WriteLine(findXorSum(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of XOR
// of all subarray of the array

// Function to calculate the sum of
// XOR of all subarrays
function findXorSum($arr, $n)
{
    // variable to store
    // the final sum
    $sum = 0;

    // multiplier
    $mul = 1;

    for ($i = 0; $i < 30; $i++)
    {

        // variable to store number of
        // sub-arrays with odd number of
        // elements with ith bits starting
        // from the first element to the
        // end of the array
        $c_odd = 0;

        // variable to check the status
        // of the odd-even count while
        // calculating c_odd
        $odd = 0;

        // loop to calculate initial
        // value of c_odd
        for ($j = 0; $j < $n; $j++)
        {
            if (($arr[$j] & (1 << $i)) > 0)
                $odd = (!$odd);
            if ($odd)
                $c_odd++;
        }

        // loop to iterate through
        // all the elements of the
        // array and update sum
        for ($j = 0; $j < $n; $j++)
        {
            $sum += ($mul * $c_odd);

            if (($arr[$j] & (1 << $i)) > 0)
                $c_odd = ($n - $j - $c_odd);
        }

        // updating the multiplier
        $mul *= 2;
    }

    // returning the sum
    return $sum;
}

// Driver Code
$arr = array(3, 8, 13);

$n = sizeof($arr);

echo findXorSum($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the sum of XOR of
// all subarray of the array

// Function to calculate the sum of XOR
// of all subarrays
function findXorSum(arr, n)
{
    // variable to store
    // the final sum
    let sum = 0;

    // multiplier
    let mul = 1;

    for (let i = 0; i < 30; i++) {

        // variable to store number of
        // sub-arrays with odd number of elements
        // with ith bits starting from the first
        // element to the end of the array
        let c_odd = 0;

        // variable to check the status
        // of the odd-even count while
        // calculating c_odd
        let odd = 0;

        // loop to calculate initial
        // value of c_odd
        for (let j = 0; j < n; j++) {
            if ((arr[j] & (1 << i)) > 0)
                odd = (!odd);
            if (odd)
                c_odd++;
        }

        // loop to iterate through
        // all the elements of the
        // array and update sum
        for (let j = 0; j < n; j++) {
            sum += (mul * c_odd);

            if ((arr[j] & (1 << i)) > 0)
                c_odd = (n - j - c_odd);
        }

        // updating the multiplier
        mul *= 2;
    }

    // returning the sum
    return sum;
}

// Driver Code
    let arr = [ 3, 8, 13 ];

    let n = arr.length;

    document.write(findXorSum(arr, n));

</script>
```

**Output:** 

```
46
```

**时间复杂度** : O(N)