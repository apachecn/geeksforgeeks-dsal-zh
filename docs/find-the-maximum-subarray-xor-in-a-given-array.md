# 求给定数组中最大子数组 XOR

> 原文:[https://www . geeksforgeeks . org/find-给定数组中的最大子数组-xor/](https://www.geeksforgeeks.org/find-the-maximum-subarray-xor-in-a-given-array/)

给定一个整数数组。求给定数组中最大 XOR 子数组值。预期时间复杂度 O(n)。

示例:

```
Input: arr[] = {1, 2, 3, 4}
Output: 7
The subarray {3, 4} has maximum XOR value

Input: arr[] = {8, 1, 2, 12, 7, 6}
Output: 15
The subarray {1, 2, 12} has maximum XOR value

Input: arr[] = {4, 6}
Output: 6
The subarray {6} has maximum XOR value
```

一个**简单的解决方法**就是用两个循环求所有子阵的 XOR，返回最大值。

## c++

```
// A simple C++ program to find max subarray XOR
#include<bits/stdc++.h>
using namespace std;

int maxSubarrayXOR(int arr[], int n)
{
    int ans = INT_MIN;     // Initialize result

    // Pick starting points of subarrays
    for (int i=0; i<n; i++)
    {
        int curr_xor = 0; // to store xor of current subarray

        // Pick ending points of subarrays starting with i
        for (int j=i; j<n; j++)
        {
            curr_xor = curr_xor ^ arr[j];
            ans = max(ans, curr_xor);
        }
    }
    return ans;
}

// Driver program to test above functions
int main()
{
    int arr[] = {8, 1, 2, 12};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Max subarray XOR is " << maxSubarrayXOR(arr, n);
    return 0;
}
```

## Java

```
// A simple Java program to find max subarray XOR
class GFG {
    static int maxSubarrayXOR(int arr[], int n)
    {
        int ans = Integer.MIN_VALUE; // Initialize result

        // Pick starting points of subarrays
        for (int i=0; i<n; i++)
        {
                // to store xor of current subarray  
            int curr_xor = 0;

            // Pick ending points of subarrays starting with i
            for (int j=i; j<n; j++)
            {
                curr_xor = curr_xor ^ arr[j];
                ans = Math.max(ans, curr_xor);
            }
        }
        return ans;
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        int arr[] = {8, 1, 2, 12};
        int n = arr.length;
        System.out.println("Max subarray XOR is " +
                                 maxSubarrayXOR(arr, n));
    }
}
//This code is contributed by Sumit Ghosh
```

## python 3

```
# A simple Python program
# to find max subarray XOR

def maxSubarrayXOR(arr,n):

    ans = -2147483648     #Initialize result

    # Pick starting points of subarrays
    for i in range(n):

        # to store xor of current subarray
        curr_xor = 0

        # Pick ending points of
        # subarrays starting with i
        for j in range(i,n):

            curr_xor = curr_xor ^ arr[j]
            ans = max(ans, curr_xor)

    return ans

# Driver code

arr = [8, 1, 2, 12]
n = len(arr)

print("Max subarray XOR is ",
     maxSubarrayXOR(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## c#

```
// A simple C# program to find
// max subarray XOR
using System;

class GFG
{

    // Function to find max subarray
    static int maxSubarrayXOR(int []arr, int n)
    {
        int ans = int.MinValue;
        // Initialize result

        // Pick starting points of subarrays
        for (int i = 0; i < n; i++)
        {
            // to store xor of current subarray
            int curr_xor = 0;

            // Pick ending points of
            // subarrays starting with i
            for (int j = i; j < n; j++)
            {
                curr_xor = curr_xor ^ arr[j];
                ans = Math.Max(ans, curr_xor);
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {8, 1, 2, 12};
        int n = arr.Length;
        Console.WriteLine("Max subarray XOR is " +
                           maxSubarrayXOR(arr, n));
    }
}

// This code is contributed by Sam007.
```

## PHP

```
<?php
// A simple PHP program to
// find max subarray XOR

function maxSubarrayXOR($arr, $n)
{

    // Initialize result
    $ans = PHP_INT_MIN;

    // Pick starting points
    // of subarrays
    for ($i = 0; $i < $n; $i++)
    {
        // to store xor of
        // current subarray
        $curr_xor = 0;

        // Pick ending points of
        // subarrays starting with i
        for ($j = $i; $j < $n; $j++)
        {
            $curr_xor = $curr_xor ^ $arr[$j];
            $ans = max($ans, $curr_xor);
        }
    }
    return $ans;
}

    // Driver Code
    $arr = array(8, 1, 2, 12);
    $n = count($arr);
    echo "Max subarray XOR is "
         , maxSubarrayXOR($arr, $n);

// This code is contributed by anuj_67.
?>
```

## Javascript

```
<script>

// A simple Javascript program to find
// max subarray XOR
function maxSubarrayXOR(arr, n)
{

    // Initialize result
    let ans = Number.MIN_VALUE;  

    // Pick starting points of subarrays
    for(let i = 0; i < n; i++)
    {

        // To store xor of current subarray
        let curr_xor = 0;

        // Pick ending points of subarrays
        // starting with i
        for(let j = i; j < n; j++)
        {
            curr_xor = curr_xor ^ arr[j];
            ans = Math.max(ans, curr_xor);
        }
    }
    return ans;
}

// Driver code
let arr = [ 8, 1, 2, 12 ];
let n = arr.length;

document.write("Max subarray XOR is " +
               maxSubarrayXOR(arr, n));

// This code is contributed by divyesh072019

</script>
```

**输出**

```
Max subarray XOR is 15
```